#To avoid the internal error due to one_hot function

**error message**

InternalError: Blas SGEMM launch failed : ~

I encountered this error while I was trying to port the jupyter notebook script from Python2 to Python3.

**my environment**

Window10 (64bit), tensorflow-gpu 0.12.1 (2016.12.25 updated version), Python 3.5

**suggested solution**

1. restart the Kernel
2. if 1 does not work, try below ([ipynb link here](https://github.com/jaejun-yoo/Three-ways-to-avoid-tf.one_hot-function-/blob/master/Three%20ways%20to%20avoid%20tf.one_hot()%20function%20.ipynb))

  1) with tf.device("/cpu:0"): # get around by using cpu at this part only
      Y = tf.one_hot(ys, 2)
      D = tf.one_hot(D_ind, 2)
  2) Define one_hot function by using other tf inbuilt functions
      #Instead of Y = tf.one_hot(ys, 2)
      num_labels = 2
      sparse_labels = tf.reshape(ys, [-1, 1])
      derived_size = tf.shape(sparse_labels)[0]
      indices = tf.reshape(tf.range(0, derived_size, 1), [-1, 1])
      concated = tf.concat(1, [indices, sparse_labels])
      outshape = tf.concat(0, [tf.reshape(derived_size, [1]), tf.reshape(num_labels, [1])])
      Y = tf.sparse_to_dense(concated, outshape, 1.0, 0.0)
  3) Define a function with numpy and use appropriate size of placeholder as a output
      def oh_encoding(label, num_classes):        
      result = np.zeros((len(label), num_classes),dtype=np.int32)
      result[np.arange(len(label)), label] = 1
      #print(result)
      return result

**referred sites**

(DANN notebook- original notebook I was trying to port from Python2 to Python3)

1. https://github.com/pumpikano/tf-dann/blob/master/Blobs-DANN.ipynb

(related to error message)

1. https://github.com/tensorflow/tensorflow/issues/6509
2. http://stackoverflow.com/questions/37337728/tensorflow-internalerror-blas-sgemm-launch-failed (the last and latest answer from this link rings the bell for me)

**Remaining issue**

After amending the code to avoid using one_hot function, the final results from the [Blobs-DANN-py2-original.ipynb](https://github.com/jaejun-yoo/Three-ways-to-avoid-tf.one_hot-function-/blob/master/Blobs-DANN-py2-original.ipynb) have changed to suspicious way..(please compare the results of the ipynb of [1st](https://github.com/jaejun-yoo/Three-ways-to-avoid-tf.one_hot-function-/blob/master/Blobs-DANN-py35-using-1st-method.ipynb), [2nd](https://github.com/jaejun-yoo/Three-ways-to-avoid-tf.one_hot-function-/blob/master/Blobs-DANN-py35-using-2nd-method.ipynb) and [3rd](https://github.com/jaejun-yoo/Three-ways-to-avoid-tf.one_hot-function-/blob/master/Blobs-DANN-py35-using-3rd-method.ipynb) methods from the original

Maybe there are other issues or maybe there is remaining problem with those substitution of one_hot function.  (still finding the way)

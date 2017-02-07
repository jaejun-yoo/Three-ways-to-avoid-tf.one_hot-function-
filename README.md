#To avoid the internal error due to one_hot function

**error message :**

InternalError: Blas SGEMM launch failed : ~

**suggested solution**

1. restart the Kernel
2. if 1 does not work, try below

I encountered this error while I was trying to port the jupyter notebook script from python2 to python3.

**referred sites:**

(DANN notebook)

1. https://github.com/pumpikano/tf-dann/blob/master/Blobs-DANN.ipynb

(related to error message)

1. https://github.com/tensorflow/tensorflow/issues/6509
2. http://stackoverflow.com/questions/37337728/tensorflow-internalerror-blas-sgemm-launch-failed (the last and latest answer from this link rings the bell for me)

**ramaining issue**

After amending the code to avoid using one_hot function, the final results from the [Blobs-DANN-py2-original.ipynb](https://github.com/jaejun-yoo/Three-ways-to-avoid-tf.one_hot-function-/blob/master/Blobs-DANN-py2-original.ipynb) have changed to suspicious way..(please compare the results of the ipynb of [1st](https://github.com/jaejun-yoo/Three-ways-to-avoid-tf.one_hot-function-/blob/master/Blobs-DANN-py35-using-1st-method.ipynb), [2nd](https://github.com/jaejun-yoo/Three-ways-to-avoid-tf.one_hot-function-/blob/master/Blobs-DANN-py35-using-2nd-method.ipynb) and [3rd](https://github.com/jaejun-yoo/Three-ways-to-avoid-tf.one_hot-function-/blob/master/Blobs-DANN-py35-using-3rd-method.ipynb) methods from the original

Maybe there are other issues or maybe there is remaining problem with those substitution of one_hot function.  (still finding the way)

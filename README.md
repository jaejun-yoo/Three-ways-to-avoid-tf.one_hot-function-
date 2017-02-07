** To avoid the internal error due to one_hot function **

error message : InternalError: Blas SGEMM launch failed :
1. restart the Kernel
2. if 1 does not work, try below

I encountered this error while I was trying to port the jupyter notebook script from python2 to python3.

referred sites:

https://github.com/tensorflow/tensorflow/issues/6509
http://stackoverflow.com/questions/37337728/tensorflow-internalerror-blas-sgemm-launch-failed (the last and latest answer rings the bell for me)

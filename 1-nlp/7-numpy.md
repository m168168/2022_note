# 11-numpy



np.r_是按列连接两个矩阵，就是把两矩阵上下相加，要求列数相等。_

_np.c_是按行连接两个矩阵，就是把两矩阵左右相加，要求行数相等。



numpy的ravel() 和 flatten()函数

ravel(散开，解开)，flatten（变平）。两者的区别在于返回拷贝（copy）还是返回视图（view），numpy.flatten()返回一份拷贝，对拷贝所做的修改不会影响（reflects）原始矩阵，

numpy.ravel()返回的是视图（view，也颇有几分C/C++引用reference的意味），会影响（reflects）原始矩阵。
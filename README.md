http://homepages.ulb.ac.be/~dgonze/TEACHING/tp_pam.html

##TP: Substitution matrices

Aim of the work

Dayhoff derived a series of substitution matrices known as PAM matrices. Those matrices can be used to compute the score of a given alignment. The choice of the substitution matrix depends on the evolutionary distance between the compared sequences. A link can been done between the evolutionary distance (in PAM unit) and the percentage of identity between the sequences. 

Because the whole series of PAM matrices are not available, it might be convenient to be able to generate any PAM scoring matrix from the PAM1 probability matrix. 

In this tutorial you are proposed to write a script (in R) to derive any PAM matrices. We provide you with the PAM1 probability matrix file (pam1.mat) and the amino acid frequency file (aafreq.mat). Note that the matrix is the probability matrix in which the values have been multiplied by 10000.
Let's go step by step

Here are the main steps you should follow:
Read data from the file (note that columns names and row names should be discarded for subsequent computation and that the values given should be divided by 10000). 

Trick: To remove the first line and first column of a file and to convert your data into a proper matrix format, you can use the following R commands:
P<-read.table(myfile, sep = "\t", header=T, colClasses=c("character",rep("integer",20)))  
        # sep specifies the type of separator you use in your file
        # header removes the first line of your file
        # colClasses allows to specify the type of variables you have in your file
P=P[1:20,2:21]  # to remove column names
P=as.matrix(P)

Compute the probability matrix corresponding to any PAM distance n (corresponding to an evolutionary distance of n PAM, i.e. the PAMn probability matrix). 

Trick: To compute the matrix product with R, you should use:
A %*% B
Since, in R, A^2 will not return the matrix product A%*%A (but will compute the square of each element separately), you should use a loop to compute the nth power of a matrix (unless you find another trick...). 
Note that it exists an efficient way to compute powers (see power.pdf) 

Compute the scoring matrix corresponding to your PAMn matrix. 

Trick: Note that by default the function log in R return the natural logarithm (base e). To get base 10 log, use the function log10:
log10(x)

Additional questions:
Check the convergence of the values in the columns of the PAM probability matrix when n becomes large: These values should approach the amino acid frequencies. 

Plot the relation between the evolutionary distance (in PAM unit) and the percentage of identity between the sequences 

Trick: The command diag(X) returns a vector which contains the diagonal elements of the matrix X:
x=diag(X)
The command sum(x) returns the sum of the elements of vector x:
s=sum(x)

Remark 

The PAM matrix can be used to artificially evolve protein sequences. This might have some applications in testing sequence analysis or phylogenetic programs. 

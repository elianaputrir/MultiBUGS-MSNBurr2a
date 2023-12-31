# MultiBUGS-MSNBurr2a
Program MultiBUGS setelah penambahan modul distribusi MSNBurr-IIa. 

## Keterangan
Modul yang telah ditambahkan dan diubah tersimpan pada folder Source code MultiBUGS-master dengan perubahan dan penambahannya terdapat pada beberapa folder berikut:
1. "MSNBurr2a.odc" dan "External.odc" pada folder Graph
2. "Randnum.odc" dan "Cumulative.odc" pada folder Math
3. "Make.odc" dan "Linking.odc" pada folder Developer
4. "Strings.odc" pada folder Doodle

Program yang sudah terkompilasi dapat di unduh pada file .zip dengan terlebih dahulu menginstal Microsoft MPI (https://docs.microsoft.com/en-us/message-passing-interface/microsoft-mpi#ms-mpi-downloads) pada komputer.

## Contoh Penggunaan
Contoh penggunaan sederhana yang dapat dilakukan dengan distribusi MSNBurr-IIa adalah dengan penerapan pada regresi dataset ketiga anscombe's quartet (https://www.kaggle.com/datasets/carlmcbrideellis/data-anscombes-quartet) dengan model yang dapat digunakan yaitu

```{r}
model{	
	for (i in 1 : N) {
		Y[i] ~ dmsnburr2a(mu[i], tau, alpha)
		mu[i] <- beta0 + beta1 * x[i]
	}
#Prior
		beta0 ~ dnorm(0, 0.01)
    		beta1 ~ dnorm(0, 0.01)
		tau ~ dgamma(0.1, 0.1)
		alpha ~ dgamma(0.1, 0.1)T(0.1,)
}

DATA
list(N=11, Y = c(7.46, 6.77, 12.74, 7.11, 7.81, 8.84, 6.08, 5.39, 8.15, 6.42, 5.73),
x = c(10.0, 8.0, 13.0, 9.0, 11.0, 14.0, 6.0, 4.0, 12.0, 7.0, 5.0))
INITIAL
INIT1
list(tau=1,alpha=1,beta0=3.1,beta1=0.51)
INIT2
list(tau=1.1,alpha=1.01,beta0=3.2,beta1=0.52)
INIT3
list(tau=1.01,alpha=1.02,beta0=3.1,beta1=0.53)
INIT4
list(tau=1.02,alpha=1.03,beta0=3.3,beta1=0.54)
```

## Referensi
Goudie, R. J. B., Turner, R. M., De Angelis, D., Thomas, A. (2020) MultiBUGS: A parallel implementation of the BUGS modelling framework for faster Bayesian inference. Journal of Statistical Software, 95(7). [doi:10.18637/jss.v095.i07](https://doi.org/10.18637/jss.v095.i07)

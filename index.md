---
title: "Graficando funciones en R"
author: "Julio César Ramírez Pacheco"
date: "30 de enero de 2017"
output: html_document
---



## Gráficos de funciones bidimiensionales

Los gráficos permiten mostrar múltiples características en una función. Los máximos, mínimos, etc., son métricas que nos dicen mucho acerca del comportamiento de una función. `R` nos permite graficar funciones de manera sencilla utilizando el concepto de vector. Por ejemplo quizás estemos interesados en conocer la forma de onda de la función seno acotada, la cual se define matemáticamente mediante la siguiente fórmula:

$$
f(t) = \begin{cases}
\sin(2 \pi t) & \mbox{para} -1 < t < 1\\
0 & \mbox{resto}.
\end{cases}
$$
Y la cual en `R` se graficaría de la siguiente manera:


```r
t  <- seq(-1, 1, length=100)
ft   <- sin(2*pi*t)           # Se calcula la función seno a partir de t
plot(t, ft, type="l", xlim=c(-4,4), ylim=c(-1.5,1.5))
grid()
```

![plot of chunk unnamed-chunk-1](figure/unnamed-chunk-1-1.png)

`R` permite añadir gráficos o puntos mediante las funciones `lines()` y `points()`. El siguiente código ejemplifica lo amterior.


```r
t  <- seq(-3,3, length=200)
f1 <- sin(2*pi*(t))
f2 <- sin(2*pi*(t-1/4))
f3 <- sin(2*pi*(t-1/2))
plot(t,f1, type= "l")
grid()
lines(t,f2, col="red")
points(t,f3,col="blue")
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2-1.png)

De igual manera se pueden definir funciones por tramos con el comando `ifelse()`, por ejemplo grafiquemos la siguiente función:

$$
f(t) = \begin{cases}
2+t & \; -2<t<-1\\
1   & \; -1<t<1\\
2-t & \;1<t<2\\
0  & \; \mbox{resto}
\end{cases}
$$


```r
t <- seq(-3,3, length=100)
ft <- ifelse(t> -2 & t < -1, 2+t, ifelse(t>= -1 & t <= 1, 1, ifelse(t>1 & t< 2, 2-t, 0)))
plot(t, ft, type = "l")
grid()
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3-1.png)

### Ejercicios:


Graficar las siguientes funciones:

$$
f(t) = \begin{cases}
1 & \; t>0\\
0 & \; \mbox{resto}
\end{cases}
$$

$$
f(t) = \begin{cases}
1+t & \; -1<t<0\\
1-t & \; 0 \le t<1\\
0 & \; \mbox{resto}
\end{cases}
$$

$$
f(t) = \begin{cases}
\mbox{e}^{-2t} & \; 0<t<2\\
1+t & \;  -1<t<0\\
0 & \; \mbox{resto}
\end{cases}
$$

## Gráficos 3D

Los gráficos en 3D permiten visualizar funciones del tipon $f(x,y)$, donde $x$ e $y$ representan variables independientes. Como ejemplo veamos la forma en la cual `R` grafica la siguiente función $f(x,y) = \sqrt{16-4x^2-y^2}$:



```r
x <- seq(-2,2,length=50)
y <- seq(-4,4, length=50)
z <- outer(x,y,function(x,y) sqrt(16-4*x^2-y^2))
```

```
## Warning in sqrt(16 - 4 * x^2 - y^2): NaNs produced
```

```r
persp(x,y,z, theta=-30, expand=0.5,ticktype = "detailed")
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4-1.png)

```r
persp(x,y,z, theta=30, expand=0.5, ticktype = "detailed")
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4-2.png)

```r
image(x,y,z)
contour(x,y,z, add=TRUE)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4-3.png)

Ejemplos: Ahora veamos la manera de hacerla con más funciones.

### Ahora para la función $z = y^2-x^2$



```r
x <- seq(-3,3,length=50)
y <- seq(-3,3, length=50)
z <- outer(x,y,function(x,y) y^2-x^2)
persp(x,y,z, theta=-30, expand=0.6, ticktype = "detailed")
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5-1.png)

```r
persp(x,y,z, theta=30, expand=0.6, ticktype = "detailed")
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5-2.png)

```r
image(x,y,z)
contour(x,y,z, add=TRUE)
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5-3.png)


### Ahora para la función $f(x,y)= (2+x^2-y^2) \mbox{e}^{1-x^2-(y^2)/4}$



```r
x <- seq(-3,3,length=50)
y <- seq(-3,3, length=50)
z <- outer(x,y,function(x,y) (2-y^2+x^2)*exp(1-x^2-(y^2)/4))
persp(x,y,z, theta=-30, expand=0.5, ticktype = "detailed")
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-1.png)

```r
persp(x,y,z, theta=30,expand=0.5,ticktype = "detailed")
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-2.png)

```r
image(x,y,z)
contour(x,y,z, add=TRUE)
```

![plot of chunk unnamed-chunk-6](figure/unnamed-chunk-6-3.png)

### Ejercicios:


![Ejercicios para graficar superficies y contornos en R.](ejercicios.png)

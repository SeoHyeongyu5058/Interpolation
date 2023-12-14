# Interpolation<br>

**개요**<br>
* [Lagrange( )]()<br>
* [MidPoint( )]()<br>



<hr>

## Lagrange( )<br>

```c
double Lagrange(double x[], double y[], int m, double xk, int o);
```
>Parameter<br>
**x[]** : x data set <br>
**y[]** : y data set <br>
**m** : The length of data set <br>
**xk** : x의 index 값
**o** : order

1. myNP.h 안에 선언되어 있다.
2. 다음과 같은 원리를 기반으로 작성되었다.<br>

$$f(x_k)=\sum_{i=0}^ny_i=\prod_{j=0,j\neq i}^n{(x-x_j)\over (x_i-x_j)}$$

* Find index k

$$x[k] \leq xq < x[k+1]$$

* caluclat for yq

$$f_i(x)={a_i\over 6h}(x_{i+1}-x)^3+{a_{i+1}\over 6h}(x-x_i)^3+({y_{i+1}\over h}-{a_{i+1}h\over6})(x-x_i)+({y_{i}\over h}-{a_{i}h\over6})(x_{i+1}-x)$$

<hr>

## Example <br>
```c++
int main()
{
    double x[] = { 1.0, 2.0, 3.0, 4.0, 5.0 };
    double y[] = { 5.0, 6.0, 9.0, 14.0, 21.0 };
    double value = 0; 

    int m = sizeof(x) / sizeof(x[0]); // 데이터 포인트의 개수
    int o = 2;
 
    for (double xk = x[0]; xk <= x[m-1]; xk += 0.1) {
        double interpolatedValue = Lagrange(x, y, m, xk, o);


        printf("Interpolated value at x=%.2f is %.4f\n", xk, interpolatedValue);

        if (xk >= x[m - 1])
            break;
    }
}
```

## Output <br>
```c
Interpolated value at x=1.00 is 5.0000
Interpolated value at x=1.10 is 5.0100
Interpolated value at x=1.20 is 5.0400
Interpolated value at x=1.30 is 5.0900
Interpolated value at x=1.40 is 5.1600
Interpolated value at x=1.50 is 5.2500
Interpolated value at x=1.60 is 5.3600
Interpolated value at x=1.70 is 5.4900
Interpolated value at x=1.80 is 5.6400
Interpolated value at x=1.90 is 5.8100
Interpolated value at x=2.00 is 6.0000
Interpolated value at x=2.10 is 6.2100
Interpolated value at x=2.20 is 6.4400
Interpolated value at x=2.30 is 6.6900
Interpolated value at x=2.40 is 6.9600
Interpolated value at x=2.50 is 7.2500
Interpolated value at x=2.60 is 7.5600
Interpolated value at x=2.70 is 7.8900
Interpolated value at x=2.80 is 8.2400
Interpolated value at x=2.90 is 8.6100
Interpolated value at x=3.00 is 9.0000
```

## Warning
>계수는 1보다 커야 한다.<br>
계수는 배열 크기보다 작아야 한다.

## Error Handling
```c
if (o < 1)
{
	printf("Order is too little.\n\n");
    return NULL;
}
else if (o > m - 1)
{
	printf("Order is should be smaller Array size.\n\n");

	return NULL;
}
```
<br>



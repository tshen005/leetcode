#
**solution**
Use divide&conquer
**time complexity**
O(logn)
**space complexity**


```cpp
class Solution {
public:
    
    double myPower(double x, int n){
        double result = 1.0;
        if(n == 0) return result;
        result = myPower(x,n/2);
        if(n % 2 == 0)
            return result*result;
        else
            return result*result*x;
    }
    
    double myPow(double x, int n) {
        if(n == 0) return 1;
        else if(n > 0) return myPower(x,n);
        else return 1/myPower(x,-1*n);
    }
};
```
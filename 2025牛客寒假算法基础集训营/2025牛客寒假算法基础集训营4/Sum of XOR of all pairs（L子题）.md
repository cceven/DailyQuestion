# [Sum of XOR of all pairs（L子题）](https://www.geeksforgeeks.org/problems/sum-of-xor-of-all-pairs0723/1?itm_source=geeksforgeeks)

![image-20250323143502691](https://gitee.com/chen-houchao/images/raw/master/202503231435768.png)

## 代码

![image-20250323143619442](https://gitee.com/chen-houchao/images/raw/master/202503231436477.png)

```cpp
//{ Driver Code Starts
// An efficient C++ program to compute 
// sum of bitwise OR of all pairs
#include <bits/stdc++.h>
using namespace std;


// } Driver Code Ends



class Solution{
    public:
    // Returns sum of bitwise OR
    // of all pairs
    long long int sumXOR(int arr[], int n)
    {
    	//Complete the function
    	long long ans=0;
    	for(int i=0;i<32;i++){
    	    int k=0;//当前为为1的个数
    	    for(int j=0;j<n;j++){
    	        if((arr[j]>>i)&1)k++;
    	    }
    	    
    	    ans+=(long long)k*(n-k)*(1<<i);
    	}
    	return ans;
    }
};


//{ Driver Code Starts.


int main()
{
	int t;
	cin>>t;
	while(t--)
	{
	 int n ;
	 cin>>n;
	 int arr[n+1];
	 for( int i=0;i<n;i++)
	    cin>>arr[i];
	 Solution ob;
	 cout<<ob.sumXOR(arr, n)<<endl;
	
cout << "~" << "\n";
}	
	return 0;
}

// } Driver Code Ends
```


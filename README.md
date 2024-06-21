Minimize the maximum difference between heights in C
Here, in this page we will discuss the program to minimize the maximum difference between heights in C . We are Given with heights of n towers and a value k. We need to either increase or decrease the height of every tower by k (only once) where k > 0. Our task is to minimize the difference between the heights of the longest and the shortest tower after modifications and output this difference.

Minimize the maximum difference between heights in C
Algorithm :
First, Sort the array and make each height of the tower maximum.
Decreasing the height of all the towers towards the right by k and increasing all the height of the towers towards the left (by k).
It is also possible that the tower you are trying to increase the height doesn’t have the maximum height.
Check whether it has the maximum height or not by comparing it with the last element towards the right side which is arr[n]-k.
Since the array is sorted if the tower’s height is greater than the arr[n]-k then it’s the tallest tower available.
Similar thing applied for finding the shortest tower.
Code in C
#include <stdio.h>
 
int min(int a, int b){
    if(a>b)
        return b;
    return a;
}

int max(int a, int b){
    if(a<b)
        return b;
    return a;
}

int getMinDiff(int arr[], int n, int k)
{
    //Sort the array
    for(int i=0; i<n; i++){
        for(int j=i+1; j<n; j++){ if(arr[i]>arr[j]){
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }

    int ans = arr[n - 1] - arr[0]; 
 
    int tempmin, tempmax;
    tempmin = arr[0];
    tempmax = arr[n - 1];
 
    for (int i = 1; i < n; i++) {
        tempmin= min(arr[0] + k,arr[i] - k); 
        tempmax = max(arr[i - 1] + k, arr[n - 1] - k); 
        ans = min(ans, tempmax - tempmin);
    }
    return ans;
}
 
// Driver Code Starts
int main()
{
    int k = 6, n = 6;
    int arr[] = { 7, 4, 8, 8, 8, 9 };
    int ans = getMinDiff(arr, n, k);
    
    printf("%d", ans);
}
Output :
5

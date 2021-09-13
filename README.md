/*
->We are given with an input array
->Choose pivot, here we are choosing the last element as our pivot
->Now partition the array as per pivot
->Keep a partitioned index say p and initialize it to -1
->Iterate through every element in the array except the pivot
->If an element is less than the pivot element then increment p and swap the elements at index p with the element at index i.
->Once all the elements are traversed, swap pivot with element present at p+1 as this will the same position as in the sorted array
->Now return the pivot index
->Once partitioned, now make 2 calls on quicksort
->One from beg to p-1
->Other from p+1 to n-1
*/




















#include<stdio.h> 

// Function to swap the elements 
void swap_elements(int* first, int* second) 
{ 
	int temp = *first; 
	*first = *second; 
	*second = temp; 
} 

int partition_function(int arr[], int l, int h) 
{ 
	int p = arr[h];
	int i = (l - 1);

	for (int j = l; j <= h- 1; j++) 
	{ 
	
		if (arr[j] < p) 
		{ 
			i++; 
			swap_elements(&arr[i], &arr[j]); 
		} 
	} 
	swap_elements(&arr[i + 1], &arr[h]); 
	return (i + 1);   
} 

void quick_sort(int arr[], int l, int h) 
{ 
	if (l < h) 
	{ 
		int p_index = partition_function(arr, l, h); 
		quick_sort(arr, l, p_index - 1); 
		quick_sort(arr, p_index + 1, h); 
	} 
} 

//Function to print the elements of the array 
void print_Array(int arr[], int len) 
{ 
	int i; 
	for (i=0; i < len; i++) 
		printf("%d ", arr[i]);  
} 

// Main Function or driver function
int main() 
{ 
	int array[] = {14, 17, 8, 90, 11, 2}; //Static array
	int length = sizeof(array)/sizeof(array[0]); //For finding the length of the array
	printf("Before Sorting the array: ");
	print_Array(array, length);
	printf("\n");
	printf("After Sorting the array: ");
       //Indexing starts from 0(zero) in array (that is why length-1)
        quick_sort(array, 0, length-1); 
	print_Array(array, length); 
	return 0; 
} 

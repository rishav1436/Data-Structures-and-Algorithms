# Examples of algorithms on arrays #

The links below go straight to the code examples. They all use the following structure:

```cpp
struct Array
{
    int size;           //represents the number of elements with user-defined values
    int length;         //represents the total number of elements currently available (must be <= 20)
    int A[20];
};
```

1. Finding the missing element in a sorted array

```cpp
void findMissingSorted(struct Array arr)
{
    int current;
    for (int i = 0; i < arr.length; i++)
    {
        if (arr.A[i+1] - arr.A[i] > 1)
        {
            cout << "Found a missing value between element: " << i << ", value change of " << arr.A[i] << " to " << arr.A[i+1] << "\n";
            return;
        }
    }
    cout << "Nothing missing here";
}
```

2. Finding multiple missing elements in a sorted array (with external array, tally, to store the starting points of missing elements)

```cpp
void findMultipleMissingSorted(struct Array arr, struct Array* tally)
{
    bool found = false;
    for (int i = 0; i < arr.length; i++)
    {
        if (arr.A[i+1] - arr.A[i] > 1)
        {
            tally->A[i] = -1;
            cout << "Found a missing value between element: " << i << ", value change of " << arr.A[i] << " to " << arr.A[i+1] << "\n";
            found = true;
        }
        else
            tally->A[i] = 0;
    }
    if (!found)
        cout << "Nothing missing here";
}
```

3. Finding duplicated elements in a sorted array

```cpp
void findDuplicates(struct Array arr)
{
    bool found = false;
    for (int i = 0; i < arr.length; i++)
    {
        if (arr.A[i+1] == arr.A[i])
        {
            cout << "Found duplicate values at elements " << i << " and " << i+1 << " with a value of " << arr.A[i] << "\n";
            found = true;
        }
    }
    if (!found)
        cout << "Nothing missing here";
}
```
4. Finding duplicated elements in a unsorted array

```cpp
void findDuplicatesUnsorted(struct Array arr)
{
    //temp records the index where the duplicate is found
    struct Array temp = {arr.size, arr.length, {0}};
    bool found = false;

    for (int i = 0; i < arr.length ; i++)
    {
        for (int j = i+1; j < arr.length; j++)
        {
            if (arr.A[i] == arr.A[j])
            {
                temp.A[i] = j;
                found = true;
                break;
            }
        }
    }

    if (found)
    {
        for (int i = 0; i < temp.length; i++)
        {
            if (temp.A[i] > 0)
            {
                cout << "Found duplicate values at elements " << i << " and " << temp.A[i] << " with a value of " << arr.A[i] << "\n";
            }
        }
    }
    else
    {
        cout << "No duplicates found";
    }
}
```

5. Finding a pair of elements with sum 'sum'

```cpp
void findPairWithSum(struct Array arr, int sum)
{
    //temp records the index where the other operand is found
    struct Array temp = {arr.size, arr.length, {0}};
    bool found = false;

    for (int i = 0; i < arr.length ; i++)
    {
        for (int j = i+1; j < arr.length; j++)
        {
            if (arr.A[i] + arr.A[j] == sum)
            {
                temp.A[i] = j;
                found = true;
                break;
            }
        }
    }

    if (found)
    {
        for (int i = 0; i < temp.length; i++)
        {
            if (temp.A[i] > 0)
            {
                cout << "Found two values at elements " << i << " and " << temp.A[i] << " with a sum of " << sum << "\n";
            }
        }
    }
    else
    {
        cout << "No operands found";
    }
}
```

6. Finding a pair of elements with sum K in a sorted array

```cpp
void findPairWithSumSorted(struct Array arr, int sum)
{
    //temp records the index where the other operand is found
    struct Array temp = {arr.size, arr.length, {0}};
    bool found = false;

    for (int i = 0; i < arr.length ; i++)
    {
        for (int j = i+1; (arr.A[i] + arr.A[j]) < sum, j < arr.length; j++)
        {
            if (arr.A[i] + arr.A[j] == sum)
            {
                temp.A[i] = j;
                found = true;
                break;
            }
        }
    }

    if (found)
    {
        for (int i = 0; i < temp.length; i++)
        {
            if (temp.A[i] > 0)
            {
                cout << "Found two values at elements " << i << " and " << temp.A[i] << " with a sum of " << sum << "\n";
            }
        }
    }
    else
    {
        cout << "No operands found";
    }
}
```

7. Finding max and min in one scan of an array

```cpp
void findMaxAndMin(struct Array arr)
{
    if (arr.length < 2)
    {
        cout << "Need an array of size >= 2" << "\n";
        return;
    }

    int minimum, maximum;
    if (arr.A[0] >= arr.A[1])
    {
        minimum = arr.A[1];
        maximum = arr.A[0];
    }
    else
    {
        minimum = arr.A[0];
        maximum = arr.A[1];
    }

    for (int i = 2; i < arr.length; i++)
    {
        if (arr.A[i] < minimum)
        {
            minimum = arr.A[i];
        }
        else if (arr.A[i] > maximum)
        {
            maximum = arr.A[i];
        }
    }
    cout << "The maximum value is " << maximum << " and the minimum value is " << minimum << "\n";
}
```
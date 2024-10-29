#include <iostream>
#include <chrono>
using namespace std;
using namespace std::chrono;

void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; ++i)
        for (int j = 0; j < n - i - 1; ++j)
            if (arr[j] > arr[j + 1])
                swap(arr[j], arr[j + 1]);
}

void selectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; ++i) {
        int minIdx = i;
        for (int j = i + 1; j < n; ++j)
            if (arr[j] < arr[minIdx])
                minIdx = j;
        swap(arr[minIdx], arr[i]);
    }
}

void merge(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1, n2 = right - mid;
    int L[n1], R[n2];
    for (int i = 0; i < n1; ++i) L[i] = arr[left + i];
    for (int i = 0; i < n2; ++i) R[i] = arr[mid + 1 + i];
    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) arr[k++] = (L[i] <= R[j]) ? L[i++] : R[j++];
    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}

void mergeSort(int arr[], int left, int right) {
    if (left >= right) return;
    int mid = left + (right - left) / 2;
    mergeSort(arr, left, mid);
    mergeSort(arr, mid + 1, right);
    merge(arr, left, mid, right);
}

int partition(int arr[], int low, int high) {
    int pivot = arr[high], i = low - 1;
    for (int j = low; j < high; ++j) {
        if (arr[j] < pivot) swap(arr[++i], arr[j]);
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

void measureTime(void (*sortFunc)(int[], int), int arr[], int n, string sortName, string caseName) {
    auto start = high_resolution_clock::now();
    sortFunc(arr, n);
    auto end = high_resolution_clock::now();
    auto duration = duration_cast<microseconds>(end - start);
    cout << sortName << " on " << caseName << " case took " << duration.count() << " microseconds.\n";
}

void measureTime(void (*sortFunc)(int[], int, int), int arr[], int low, int high, string sortName, string caseName) {
    auto start = high_resolution_clock::now();
    sortFunc(arr, low, high);
    auto end = high_resolution_clock::now();
    auto duration = duration_cast<microseconds>(end - start);
    cout << sortName << " on " << caseName << " case took " << duration.count() << " microseconds.\n";
}

int main() {
    const int n = 1000;
    int bestCase[n], averageCase[n], worstCase[n];
    for (int i = 0; i < n; ++i) bestCase[i] = i;
    for (int i = 0; i < n; ++i) averageCase[i] = rand() % n;
    for (int i = 0; i < n; ++i) worstCase[i] = n - i;

    measureTime(bubbleSort, bestCase, n, "Bubble Sort", "Best");
    measureTime(bubbleSort, averageCase, n, "Bubble Sort", "Average");
    measureTime(bubbleSort, worstCase, n, "Bubble Sort", "Worst");

    measureTime(selectionSort, bestCase, n, "Selection Sort", "Best");
    measureTime(selectionSort, averageCase, n, "Selection Sort", "Average");
    measureTime(selectionSort, worstCase, n, "Selection Sort", "Worst");

    measureTime(mergeSort, bestCase, 0, n - 1, "Merge Sort", "Best");
    measureTime(mergeSort, averageCase, 0, n - 1, "Merge Sort", "Average");
    measureTime(mergeSort, worstCase, 0, n - 1, "Merge Sort", "Worst");

    measureTime(quickSort, bestCase, 0, n - 1, "Quick Sort", "Best");
    measureTime(quickSort, averageCase, 0, n - 1, "Quick Sort", "Average");
    measureTime(quickSort, worstCase, 0, n - 1, "Quick Sort", "Worst");

    return 0;
}

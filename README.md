# JIMS
Javascript Interactive Merge Sort.

The sorting algorithm where you are the compare function.

## Goal
This small JS library is useful when trying to sort or prioritize a list of items for which the comparison operation is transitive but cannot be determined algorithmcally.
Ie:
```
a < b and b < c => a < c
```
but a computer cannot tell that `a < b`.

In that case, the two items are displayed to the user which acts as a compare function by selecting which one holds a greater value. Based on these comparisons, the library performs merge sort in the background.

For example, I use it to sort my list of video games played and determine my top 10. You can find the demo [here](https://abrochard.github.io/game-timeline/sort.html).

## Usage
The library can be used a such:
```
var sorter = new Jims(elements, displayLeft, displayRight, showResult, top);
```
where
- `elements` is an array of elements to sort
- `displayLeft` and `displayRight` are functions taking as a parameter an item out of the elements array and display that element on the left or right side of the screen respectively
- `showResult` is the callback function that will be called with the sorted list of elements once the process is done
- `top` is an optional parameter indicating that you only care about the top n elements of the array to sort. Note that a smaller top means less comparison for the user as lower valued elements are discarded. By default, `top` is set to the length of `elements`

The `sorter` object then provides two picker functions which you should hook up to the user's click on the left and right side element respectively:
```
var picker = sorter.pickerFunctions();

$('#left').click(picker.left);
$('#right').click(picker.right);
```
Once triggered, these picker functions will step forward with the comparison and use the `displayLeft` and `displayRight` functions to present a new combination to the user.

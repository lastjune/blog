#排序


###Bucket Sort-桶排序 O(n)

排序思路是,例如对`[1,3,4,6,7,15]`进行排序
首先新建一个长度为16的数组，遍历原数组，将1插入新数组，下标为1的位置，3插入下表为3的位置

###Bubble Sort-冒泡排序O(n²)

```javascript

let ary=[3,1,5,15,7,6];
let temp;
for(var i=ary.length-1;i>=0;i--){
    for(var j=1;j<=i;j++){
        if(ary[j-1]>ary[j]){
            temp=ary[j-1];
            ary[j-1]=ary[j];
            ary[j]=temp;
        }
    }
}
console.log(ary);//[ 1, 3, 5, 6, 7, 15 ]
```

###Selection Sort-选择排序O(n²)

选择排序的思路是，依次遍历数组的每一个元素，将这个元素与它之后的每一个元素做比较，如果寻找到比该元素小的元素，则记录最小元素下标，在循环结束时判断若下标与元素下标不同，则调换两个元素，执行下一个元素流程。

```javascript

var ary = [3, 1, 5, 15, 7, 6];
var select = function(ary) {
    var aLength = ary.length;

    if (aLength < 2) {
        return ary;
    }

    for (var i = 0; i < aLength-1; i++) {
        var index = i;
        for (var j = i + 1; j < aLength; j++) {
            if (ary[j] < ary[index]) {
                index = j;
            }
        }

        if (i !== index) {
            var temp = ary[i];
            ary[i] = ary[index];
            ary[index] = temp;
        }
    }

    return ary;
}

console.log(select(ary)); //[ 1, 3, 5, 6, 7, 15 ]

```
###Insertion Sort-插入排序O(n²)

```javascript

```

###Quick Sort-快速排序

快速排序的思想是使用递归的方式,先取一个数作为基数，
然后遍历数组，比基数小的放入left数组，比基数大的放入right数组
遍历完之后，继续递归left与right

```javascript

let ary=[3,1,5,15,7,6];
var quick=(ary)=>{
    let aLength=ary.length;
    let pivotIndex=Math.floor(ary/2);
    let pivot=ary.splice(pivotIndex,1)[0];

    let left=[];
    let right=[];

    if(aLength<2){
        return ary;
    }
    for(var i=0;i<ary.length;i++){
        if(ary[i]<pivot){
            left.push(ary[i]);
        }
        else{
            right.push(ary[i]);
        }
    }
    return arguments.callee(left).concat(pivot,arguments.callee(right));

}
console.log(quick(ary));

```

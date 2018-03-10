## 基础排序

直接上代码：

```javascript
class CArray {
    constructor(numElements){
        // 存储数据的数据
        this.dataStore = [];
        // 位置
        this.pos = numElements || 0;
        // 传入的数组的大小
        this.numElements = numElements;

        this.init();
    }
    // 初始化数组的数据
    init () {
        for(let i = 0; i < this.numElements; i++){
            this.dataStore[i] = i;
        }
    }
    // 设置数据
    setData () {
        for(var i = 0; i < this.numElements; i++){
            this.dataStore[i] = Math.floor(Math.random() * (this.numElements +1)); // 随机设置数组内元素的大小
        }
    }
    // 输出数据
    toString () {
        var restr = "";
        for(var i = 0; i < this.dataStore.length; i++){
            restr += this.dataStore[i] + " ";
            if(i > 0 && i % 10 == 0){
                restr += "\n";
            }
        }
        return restr;
    }
    // 清除数据
    clear () {
        for (var i = 0; i < this.dataStore.length; i++){
            this.dataStore[i] = 0;
        }
    }
    // 交换两个数据
    swap (arr , index1 ,index2) {
        var temp = arr[index1];
        arr[index1] = arr[index2];
        arr[index2] = temp;
    }
    //  在数组后面插入数据的方法
    insert (element) {
        this.dataStore[this.pos++] = element;
    }
    // 冒泡排序
    bubbleSort () {
        var numElements = this.dataStore.length;
        for(var outer = numElements; outer >=2; outer--){
            for(var inner = 0; inner <= outer-1; inner++){
                if(this.dataStore[inner] > this.dataStore[inner + 1]){
                    this.swap(this.dataStore,inner,inner+1);
                }
            }
        }
    }
    // 选择排序
    selectionSort () {
        var min; //最小元素的下标
        for(var outer = 0; outer <= this.dataStore.length - 2; outer++){
            min = outer;
            for(var inner = outer+1; inner <= this.dataStore.length-1; inner++){
                if(this.dataStore[inner]< this.dataStore[min]){
                    min = inner;
                }             
            }
            this.swap(this.dataStore, outer, min);
        }
    }
    // 插入排序
    insertionSort () {
        var temp , inner;
        for(var outer = 1; outer <= this.dataStore.length - 1; outer++){
            temp = this.dataStore[outer];
            inner = outer;
            while(inner > 0 && (this.dataStore[inner-1] >= temp)) {
                this.dataStore[inner] = this.dataStore[inner - 1];
                inner--;
            }
            this.dataStore[inner] = temp;
        }
    }
    // 快速排序
    quickSort (list) {
        if(list.length == 0){
            return [];
        }
        var lesser = [];
        var greater = [];
        var pivot = list[0];
        for(var i = 1; i < list.length; i++){
            if(list[i] < pivot) {
                lesser.push(list[i]);
            }else{
                greater.push(list[i]);
            }
        }
        return this.quickSort(lesser).concat(pivot,this.quickSort(greater));
    }
}

// var numElements = 10;
// var myNums = new CArray(numElements);
// myNums.setData();
// 基础排序
// myNums.bubbleSort(); // 冒泡排序
// myNums.selectionSort(); // 选择排序
// myNums.insertionSort(); // 插入排序
 console.log(myNums.quickSort([3,2,5,1,6,3])); // 快速排序
// console.log(myNums.toString());
```

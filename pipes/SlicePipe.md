# 介绍
[api-doc](https://angular.io/api/common/SlicePipe)

SlicePipe管道作用于列表或字符串，用来截取其中一部分显示。
语法:
```
数组或字符串表达式 | slice:start[:end]
```
- start：必须的参数，只能接受正整数、负整数和0。表示从数组和字符串的哪个位置开始切片，切片中包含start位置的元素或字符；
> - 正整数：表示从数组或字符串从前往后第几个位置开始切片。
> - 0：表示从数组或字符串的第一个位置开始切片。
> - 负整数：表示从数组或字符串倒数第几个位置开始切片。
> - 如果start为正数，并且大于数组或字符串的长度，那么切片将返回空数组或空字符串。
> - 如果start为负数，并且start的绝对值大于数组或字符串的长度，那么切片将返回整个数组或字符串。
- end：可选参数，只能接受正整数、负整数和0。表示切片的结束位置，注意end的位置元素不包含。
> - 没有设置end：表示从start位置切片到末尾，包含最后一个元素或字符。
> - 正整数：表示切片的结束位置为从前到后的第几个位置。
> - 负整数：表示切片的结束位置为倒数第几个位置。
> - 0：切片将返回空数组或空字符串。

>*底层是通过Array.prototype.slice()和String.prototype.slice()实现的。*  
>*针对数组，除了返回整个数组，其他情况都是返回一个新的数组，而不是原始的数组对象*
>*如果数组为空或者空字符串，那么也将返回空数组或空字符串*

# 数组用法
```typescript
@Component({
  selector: 'slice-list-pipe',
  template: `<ul>
    <li *ngFor="let i of collection | slice:1:3">{{i}}</li>
  </ul>`
})
export class SlicePipeListComponent {
  collection: string[] = ['a', 'b', 'c', 'd'];
}
```
结果显示为
- b
- c

# 字符串用法
```typescript
@Component({
  selector: 'slice-string-pipe',
  template: `<div>
    <p>{{str}}[0:4]: '{{str | slice:0:4}}' - output is expected to be 'abcd'</p>
    <p>{{str}}[4:0]: '{{str | slice:4:0}}' - output is expected to be ''</p>
    <p>{{str}}[-4]: '{{str | slice:-4}}' - output is expected to be 'ghij'</p>
    <p>{{str}}[-4:-2]: '{{str | slice:-4:-2}}' - output is expected to be 'gh'</p>
    <p>{{str}}[-100]: '{{str | slice:-100}}' - output is expected to be 'abcdefghij'</p>
    <p>{{str}}[100]: '{{str | slice:100}}' - output is expected to be ''</p>
  </div>`
})
export class SlicePipeStringComponent {
  str: string = 'abcdefghij';
}
```

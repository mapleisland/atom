# gulp
gulp的作用就是**帮我们完成某些任务**  
gulp最擅长的就是

- 给自己安排任务:`task`
- 将自己的大任务划分为可以独立执行的小任务,并且知道在执行这个大任务时有哪些小任务需要事先先被执行
- 设置要操作的文件:`src`
- 任务中让一个步骤接着一个步骤依次执行:`pipe`
- 任务中的步骤怎么做:`pipe中调用的方法`
- 设置操作后文件的去处:`dest`
- 监视文件:`watch`

---

### 设置一个任务
一个简单任务:把大象放进冰箱里
```javascript
gulp.task('put-elephant-into-fridge', function() {
  console.log('打开冰箱门');
  console.log('把大象放进冰箱里');
  console.log('关上冰箱门');
  console.log('大象放进去啦!');
});
```

一个包含任务列表的任务
```javascript
gulp.task('default', ['open-the-door','push-elephant-into-the-fridge','close-the-door'], function() {
  console.log('大象放进去啦!');
});
```

```javascript
gulp.task('open-the-door', function() {
  console.log('打开冰箱门');
});

gulp.task('push-elephant-into-the-fridge', ['open-the-door'], function() {
  console.log('把大象放进冰箱里');
});

gulp.task('close-the-door', function() {
  console.log('关上冰箱门');
});

gulp.task('default', ['open-the-door','push-elephant-into-the-fridge','close-the-door'], function() {
  console.log('大象放进去啦!');
});
```

```javascript
gulp.src()
//gulp.src()设置任务的源文件

gulp.dest()
//gulp.dest()设置任务的目标文件

gulp.watch()
//gulp.watch()设置监视的条件
```

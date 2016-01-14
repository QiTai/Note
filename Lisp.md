# Notes from Structure and Interpretation of Computer Programs
  + Keywords
   * newline diplay square map length filter cons car cdr list lambda cond or and not let if begin else cadr ' set!
   * pair? even? odd? null? eq? equal? 
   
  + Grammar
 
  ```
  //条件判断
  (cond (<p1> <e1>)
        (<p2> <e2>)
        (else <e3>))
  
  (if <predicate> 
      <consequent> 
      <alternative>)
  (and <e1> … <en>) 
  (or  <e1> … <en>)
  (not <e>)
  
  //用lambda创建过程
  (lambda (<formal-parameter>) <body>)  e.g. : (lambda (x) (+ x 4))
  
  //用let创建局部变量
  (let (<var1> <exp1>)
       (<var2> <exp2>)
       ...
       (<varn> <expn>))
       <body>)
  //表结构数据（序对）
  (cons n d)
  (car ..)     
  (cdr ..)    
  (cadr ..)  
  (caddr ..)
  
  //序列的表示
  (list <a1> <a2> <a3> … <an>) <=>  (cons <a1> (cons <a2> (cons <a3> (cons …( … (cons <an> nil)))))
  
  //map操作
  
  //层次性结构:用list构建树
  (cons (list 1 2) (list 3 4))
  
  //序列操作：用信号流的方式处理问题
  
  //符号变量： '   

  //检查两个符号是否相等： eq?

  (put <op> <type> <item>)

  (get <op> <type>)

  //赋值
  (set! <name> <new-value> )

  //顺序执行：
  (begin <exp1> <exp2>) : 最后一个表达式<exp.>的值又将作为整个begin形式的值返回。

  //针对序对的基本改变函数set-car!和set-cdr!
  //(set-car! x y)就是将x的car用y的值来取代
  //由此可以看出，对于表的改变函数可能创建“垃圾”，Lisp的存储管理系统中包含着一个垃圾收集器。

  //检查表结构是否共享的一种方式是使用谓词eq?
  ```
  
  + Miscellany
   * [SICP习题集](http://sicp.readthedocs.org/en/latest/index.html)
   * 使用[trace](http://sicp.readthedocs.org/en/latest/chp1/6.html)来跟踪一个函数调用过程
   * [MIT Scheme基本使用](http://www.math.pku.edu.cn/teachers/qiuzy/progtech/scheme/mit_scheme.htm)
  
  
  

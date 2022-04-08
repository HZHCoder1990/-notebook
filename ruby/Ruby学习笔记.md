#### Ruby学习笔记

- 进入调试界面

​      控制台输入: irb

- 一些方法

  ```ruby
  1.methods  # 查看对象所有的方法
  1.nil? # 查看对象是否为nil 返回值是一个boolean
  "".empty # 判断字符串是否为空串
  system "say 妈妈问我怎么不开心" # 播放语音 system "say 后面跟内容"
  
  2..5  # [2,5] 闭区间
  2...5 # [2,5) 左闭右开区间
  
  input = gets.chomp.to_i # chomp 格格地咬牙，咬响牙齿；切齿 这里的作用是去除换行符
  if input == 10
      puts "123"
  end
  
  # 异常处理
  a = 100
  while true
      b = gets.chomp.to_i
      begin 
          # 把可能出现异常的代码放在这里
          puts a / b
      rescue Exception => e
          puts "请不要输入0"
      end
  end
  
  #--------------------
  # 类的拓展
  class Student
      def initialize(name)
          @name = name
      end
  end
  
  class Student 
      Version = "0.0.1"
      def sayName
          puts @name
      end
  
      def self.hello
          puts "我是类方法的拓展"
      end
  end
  
  stu = Student.new("黄先生")
  stu.sayName
  Student.hello
  # 类变量
  puts Student::Version
  #----------------
  ```

  ```ruby
  def each_start_with(a, b)
      a.each { |num|
         if num.start_with?(b)
           yield num
         end 
      }
  end
  
  each_start_with(["abc","abcd","as"], "ab") { |s|
    puts s
  }
  
  # 改写过后
  def each_start_with(a, b)
      a.each do |num|
         yield num if num.start_with?(b)
      end
  end
  
  each_start_with(["abc","abcd","as"], "ab") { |s|
    puts s
  }
  ```

- Self

  ```ruby
  class Point 
      # 对外提供的setter和getter方法
      attr_accessor :x # 可读写
      attr_reader :y # 只能读  attr_writer 只能写
      def initialize(x = 0, y = 0)
          @x, @y = x, y
      end
  
      def first_quadrant?
          # 这里能直接写 x 和y 的原因是 写了 attr_accessor 并且省略了self
          x > 0 && y > 0
          # 如果想调用x的setter方法 最好写成 self.x = 3 or @x = 3 因为ruby不知道 x是否是 local variable
      end
    
      def +(p2)
          Point.new(x + p2.x, y + p2.y)
      end
  end
  ```

- 查看某个类的方法

  ```ruby
  # irb 控制台
  [].methods.grep /^re/
  ```
  
- Module中的类

  ```ruby
  module M
      class C
          X = "constant"
      end
      puts C::X # constant
  end
  
  puts M::C::X # constant
  ```
  
- 类方法

  ```ruby
  # Ruby中定义类方法
  
  # 第一种:  class << 类名 ~ end
  class << Person
  
      def run(name)
          puts "#{name},--run"
      end
  end
  Person.run("Mr.黄先生")
  
  # 第二种 class << self ~ end
  class Person
      class << self
          def run(name)
              puts "#{name},--run"
          end
      end
  end
  Person.run("Mr.黄先生")
  
  # 第三种 def 类名.类方法 ~ end
  class Person
      def self.run(name)
          puts "#{name},--run"
      end
  end
  Person.run("Mr.黄先生")
  
  #第四种 类似于第三种
  class Person
      def Person.run(name)
          puts "#{name},--run"
      end
  end
  Person.run("Mr.黄先生")
  
  # 第五种
  class Person
      Person.instance_eval do 
          def run(name)
              puts "#{name},--run"
          end
      end
  end
  Person.run("Mr.黄先生")
  ```
  
  ```ruby
  # Example
  class Person
  
      def age
          @@age
      end
  
      def logAge(age)
          @@age = age
      end
  
      class << self
  
          # 相当于类变量 不是实例变量
          attr_accessor :name
  
          def run(name)
              @name = name
              puts "#{name},--run"
          end
      end
  end
  Person.run("Mr.黄先生")
  # 可以直接取到
  Person.name = "Mr.哈哈"
  puts Person.name
  
  p = Person.new
  p.logAge(20)
  puts p.age
  ```
  
  记录
  
  ```ruby
  class Person
      class << self
         # 类实例
          attr_accessor :name
      end
      def self.run(name)
          self.name = name
          puts self # Person 
      end
  
      def test
          puts self # #<Person:0x0000000100ed84f0> instance
      end
  end
  Person.run("asda")
  puts Person.name
  
  per = Person.new
  per.test
  
  # ------------------ HASH
  h1 = {:name => "黄先生", :age => 30}
  h2 = h1.merge({:height => 170}) # 对象地址变了
  
  h3 = {name: 1}
  h4 = {:name => 2}
  puts h3[:name]
  puts h4[:name]
  
  {name => aada} # 错误的 ❎
  
  #----------
  module ModuleA
  
      class Command
          def initialize(arguments)
              @arguments = arguments
          end
      end
  end
  
  module ModuleA
      module TEST
          # 这里也能拿到Command中的arguments
          def log
              @arguments.each do |x|
                  puts x
              end
          end
      end
  end
  
  ModuleA::Command.send(:include, ModuleA::TEST)
  
  cmd = ModuleA::Command.new(["Mr.黄先生", "哈哈", 1])
  cmd.log
  
  #----
  # *args 是一个数组
  def log(*args)
      args.each do |x|
          puts x
      end
  end
  log(["Mr黄先生", 1,"哈哈"])
  ```
  
  
  
  <img src="/Users/mac/Library/Application Support/typora-user-images/image-20220331170534258.png" alt="image-20220331170534258" style="zoom:50%;" />
  
  https://blog.csdn.net/zyhmz/article/details/82962537
  
  ```ruby
  a = '--exclude-pods=RxSwift=123=456'
  # 把整个字符串分割为2部分 选取第一个'='作为分隔符
  puts a[2..-1].split('=', 2)
  # exclude-pods
  # RxSwift=123=456
  ```
  
  ```ruby
  a = [1,2,3,'hello',4,5]
  while argument = a.shift
      next if argument == 'hello' # 类似 continue 跳出本次循环
      puts argument
  end
  # 1
  # 2
  # 3
  # 4
  # 5
  ```
  
- Ruby中的`tap`操作

  https://www.jianshu.com/p/44bde59393e6
  
  

# Java構文
- [1. コメント](#1-コメント)
- [2. 変数宣言](#2-変数宣言)
- [3. 条件分岐](#3-条件分岐)
- [4. 繰り返し](#4-繰り返し)
- [5. 配列](#5-配列)
- [6. メソッド](#6-メソッド)
- [7. 複数クラス、ファイル分割](#7-複数クラスファイル分割)
- [8. インスタンスとクラス](#8-インスタンスとクラス)
- [9. コンストラクタ](#9-コンストラクタ)
- [10. 継承](#10-継承)
- [11. 高度な継承](#11-高度な継承)
- [12. 多態性](#12-多態性)
- [13. カプセル化](#13-カプセル化)
- [14. Javaを支えるクラス](#14-javaを支えるクラス)
- [15. コレクション](#15-コレクション)
- [16. 例外](#16-例外)
  

## 1. コメント
複数行コメント  
```java
/* コメント本文 */
```

単一行コメント  
```java
// コメント本文
```

## 2. 変数宣言
通常の変数宣言  
```java
型 変数名;
型 変数名 = データ;
```  
  
定数の宣言  
```java
final 型 定数名 = 初期値;
```
  
### 型一覧
| 分類   | 型名    | 格納するデータ   |
| :----- | :------ | :--------------- |
| 整数   | byte    | とても小さな整数 |
| 整数   | short   | 小さな整数       |
| 整数   | int     | 普通の整数       |
| 整数   | long    | 大きな整数       |
| 小数   | float   | 曖昧でもよい少数 |
| 小数   | double  | 普通の数         |
| 真偽値 | boolean | true or false    |
| 文字   | char    | 一つの文字       |
| 文字列 | String  | 文字の並び       |

## 3. 条件分岐
### if
```java
if (条件式) {
    ブロック
} else if(条件式){
    ブロック
} else {
    ブロック
}
```

### switch
```java
switch(fortune) {
    case 1:
        System.out.println(str1)
        break:
    case 2:
        System.out.println(str2)
        break:
    case 3:
        System.out.println(str3)
        break:
    default:
        System.out.println(str4)
}
```

## 4. 繰り返し
### while
```java
while (条件式) {
    ブロック
}
```

### do-while
```java
do {
    ブロック
} while(temp > 25);
```

### for
```java
for (int i = 0; i < 10; i++) {
    ブロック
}
```

### 拡張for文
配列を回す方法
```java
for (int value : array) {

}
```

### break
繰り返し自体を中断
```java
for (int i = 0; i < 10; i++) {
    ブロック
    break;
}
```

### continue
今回の周だけ中断し次の周へ
```java
for (int i = 0; i < 10; i++) {
    ブロック
    continue;
}
```

## 5. 配列
### 宣言①
```java
int[] array;
array = new int[5];
```

### 宣言②
```java
int[] array = new int[5];
```

### 初期化
自動的に初期化される。
| 型       | 初期値 |
| :------- | :----- |
| 数値の型 | 0      |
| boolean  | false  |
| 文字の型 | null   |

### 宣言+代入
```java
int [] array1 = new int[] {20, 30, 40, 50, 80}; //方法①
int [] array2 = {20, 30, 40, 50, 80}; //方法②
```

### 配列の参照停止
```java
array = null;
```

### 多次元配列
```java
int[][] array = new int[] ];
```

## 6. メソッド
### メソッドの定義と呼び出し
```java
public class Main {
    public static void main(String[] args) {
        int ans = add(100, 20); //呼び出し: method(arg1, arg2..)
        System.out.println(ans);
    }

    // 定義: public static 戻り値の型　method(型 arg1, 型 arg2) {
    public static int add(int x, int y) {
        int ans = x + y;
        return ans;
    }
}
```
### オーバーロード
仮引数が異なれば同じ名前のメソッドを複数定義できる。
```java
public class Main {
    public static int add(int x, int y) {
        return x + y;
    }
    public static double add(double x, double y) {
        return x + y;
    }
    public static int add(int x, int y, int z) {
        return x + y + z;
    }
    public static void main(String[] args) {
        System.out.println(add(10, 20));
        System.out.println(add(10.4, 20.4));
        System.out.println(add(10, 20, 30));
    }
}
```

### 引数、戻り値に配列を用いる
配列の先頭アドレスの参照渡しとなる。
```java
public class Main {
    public static void printArray(int[] array) {
        for (int element : array) {
            System.out.println(element);
        }
    }
    public static void main(String[] args) {
        int[] array = {1, 2, 3};
        printArray(array);
    }
}
```
```java
public class Main {
    public static int[] makeArray(int size) {
        int[] newArray = new int[size];
        for (int i = 0; i < size; i++) {
            newArray[i] = i;
        }
        return newArray;
    }
    public static void main(String[] args) {
        int[] array = makeArray(3);
        for (int i : array) {
            System.out.println(i);
        }
    }
}
```
### コマンドライン引数
コマンドライン引数を利用したJavaプログラムの起動
```bash 
java Main arg1 arg2
# JVMによって配列に変換されmainメソッド起動時に渡される
```

## 7. 複数クラス、ファイル分割
### 他クラス（ファイル）のメソッドの呼び出し
型 変数名 = Class名.method();
```java
int total = CalcLogic.tasu(a, b);
```
呼び出し元
```java
public class CalcLogic {
    public static int tasu(int a, int b) {
        return (a + b);
    }
    public static int hiku(int a, int b) {
        return (a - b);
    }
}
```
### パッケージの作成
クラスをパッケージに所属させる。
package 所属させたいパッケージ名;
```java
package calcapp.logics;
public class Calc {
    ...
}
```
### 別のパッケージにあるクラスの呼び出し
①パッケージ名.クラス名
```java
package calcapp.main;

public class Calc {
    public static void main(String[] args) {
        int a = 10; int b = 2;
        int total = calcapp.logics.CalcLogic.tasu(a, b)
        int total = calcapp.logics.CalcLogic.hiku(a, b)
        System.out.println(total)
        System.out.println(delta)
    }
}
```
②import パッケージ名.クラス名;
```java
package calcapp.main; 
import calcapp.logics.CalcLogic// $CLASSPATH/calcapp/logics/CalcLogic

public class Calc {
    public static void main(String[] args) {
        ...
        // int total = calcapp.logics.CalcLogic.tasu(a, b)
        int total = CalcLogic.tasu(a, b)
        // int total = calcapp.logics.CalcLogic.hiku(a, b)
        int total = CalcLogic.hiku(a, b)
        ...
    }
}
```
③パッケージ内の全クラスのインポート
```java
package calcapp.main;
import calcapp.logics.*; // $CLASSPATH/calcapp/logics/*

public class Calc {
    ...
}
```


## 8. インスタンスとクラス
### クラスの定義
```java
public class Hero { // クラスを宣言
    // 属性=フィールドの定義
    String name;
    int hp;
    // 操作=メソッドの定義
    public void sleep() {
        this.hp = 100;
        system.out.println(this.name + "は、眠って回復した"); //自分自身のフィールド呼び出し
    }
    public void sit(int sec) {
        this.hp += sec;
        System.out.println(this.name + "は、" + sec + "秒座った!")
        System.out.println("HPが、" + sec + "ポイント回復した")
    }
    public void run() {
        System.out.println(this.name + "は逃げ出した!");
        System.out.println("最終HPは" + this.hp + "でした");
    }
}
```
クラス名、メンバ名のルール
| 対象         | 品詞 | 記法                       | 例                    |
| :----------- | :--- | :------------------------- | :-------------------- |
| クラス名     | 名詞 | 単語の頭が大文字           | Hero, MonsterInfo     |
| フィールド名 | 名詞 | 最初以外の単語の頭が大文字 | level, itemList       |
| メソッド名   | 動詞 | 最初以外の単語の頭が大文字 | attack, findWeakPoint |

### インスタンスの定義、フィールド・メソッドの利用
クラス名　変数名 = new クラス名();
変数名.フィールド名 = 値;
```java
public class Main {
    public static void main(String[] args) {
        // インスタンスの生成
        Hero h = new Hero();
        // フィールドに初期値をセット
        h.name = "ミナト"
        h.hp = 100
        System.out.println(h.name)
        // メソッドの呼び出し
        h.sit(5);
        h.slip();
        h.sit(25);
        h.run();
    }
}
```

### クラス型を用いる
フィールドに用いる
```java
public class Main {
    public static void main(String[] args){
        Sword s = new Sword();
        s.name = "炎の剣";
        s.damage = 10;
        h.name = "ミナト";
        h.hp = 100;
        h.sword = s;
        System.out.println("現在の武器は" + h.sowrd.name);
    }
}
```
引数に用いる
```java
public class Wizard {
    String name;
    int hp;
    public void heal(Hero h) {
        h.hp +=10;
    }
}
```

## 9. コンストラクタ
newされた直後に自動的に実行されるメソッド
public クラス名() {
    自動的に実行する処理
}
```java
puclic class Hero {
    String name;
    int hp;

    public Hero(String name) {
        this.hp = 100;
        this.name = name;
    }
}
```
Heroクラスの呼び出し
```java
public class Main {
    public static void main(String[] args) {
        Hero h = new Hero("ミナト");
    }
    System.out.println(h.hp); // 100
    System.out.println(h.name); // ミナト
}
```
### コンストラクタのオーバーロード
```java
public class Hero {
    String name;
    int hp;

    public Hero(String name) {
        this.hp = 100;
        this.name = name;
    }
    public Hero() {
        this.hp = 100;
        this.name = "ダミー";
    }
}
```
### 他のコンストラクタを呼び出す
```java
public class Hero {
    String name;
    int hp;

    public Hero(String name) {
        this.hp = 100;
        this.name = name;
    }
    public Hero() {
        this("ダミー"); // this.Hero("ダミー")ではない
    }
}
```

## 10. 継承
puclic class クラス名 extends 親クラス名 {
    親クラスとの差分メンバ
}
```java
public class SuperHero extends Hero {
    boolean flying;
    public void fly(){
        this.flying = true;
        System.out.println("飛び上がった");
    }
    public void land() {
        this.flying = false;
        System.out.println("着地した");
    }
}
```
※ javaでは多重継承は許可されていない
### オーバーライド
親クラスに同じメンバがあれば、そのメンバは「上書き変更」される。
```java
public class SuperHero extends Hero {
    boolean flying;
    public void fly(){
        this.flying = true;
        System.out.println("飛び上がった");
    }
    public void land() {
        this.flying = false;
        System.out.println("着地した");
    }
    public void run() { //親クラスでも定義されている
        System.out.println(this.name + "は撤退した");
    }
}
```
### 継承、オーバーライドの禁止
- クラス宣言時にfinalをつけると、継承禁止となる。
- メソッド宣言時にfinalをつけると、オーバーライド禁止となる。
```java
public final class Main {
    public static void main(String[] args) {
        // メインメソッド
    }
}
```
```java
public class Hero{
    ...
    public final void slip() {
        this.hp -= 5;
    }
    ...
}
```
※ フィールドはオーバーライドさせない
### 親クラスのフィールド、メソッドの呼び出し
super.フィールド名;
super.メソッド名(引数);
```java
public class SuperHero extends Hero {
    public void attack(Matango m) {
        super.attack(m); // 親インスタンス部のattack()の呼び出し
        if (this.flying) {
            super.attack(m); // 親インスタンス部のattack()の呼び出し
        }
    }
}
```
※ 親の親のインスタンス部分にはアクセスできない  

### 継承を利用したクラスのコンストラクタ
```java
public SuperHero() {
    super(); // 親クラスのコンストラクトを呼び出す
    ...
}
```

## 11. 高度な継承
### 抽象メソッドの宣言
public abstract 戻り値の型 メソッド名(引数リスト);  
- 詳細未定のメソッドを記述する構文
```java
public class Character {
    ...
    public abstract void attack(Matango m); //抽象メソッドの宣言
}
```

### 抽象クラスの宣言
- 抽象メソッドを１つでも含むクラスは、抽象クラスとして宣言する
- 抽象クラスは、newによるインスタンス化が禁止される
```java
public abstract class Character { // 抽象クラスの宣言
    String name;
    int hp;
    public void run() {
        System.out.println(this.name + "は逃げ出した");
    }
    public abstract void attack(Matango m);
}
```
### インターフェース
次の条件を満たす抽象クラスをインターフェースとして特別に扱うことができる
- すべてのメソッドは抽象メソッドである。
- 基本的にフィールドを1つも持たない
ex)
```java
public abstract class Creature {
    public abstract void run();
}
```
宣言方法  
public interface インターフェース名 {  
    ...  
}  
```java
public interface Creature {
    public abstract void run();
}
```
「public abstract」が不要になるので下記でも良い
```java
public interface Creature {
    void run();
}
```
※ インターフェースでフィールドを定義すると、「public static final」がついた定数となる。

### インターフェースの実装  
public class クラス名 ***implements*** インターフェース名 {  
    ...  
}  
```java
public class kyotoCleaningShop implements CleaningService{
    String ownerName;
    ...
    public Shirt washShirt(Shirt s) {
        return s;
    }
    ...
}
```

### インターフェースを多重継承
インターフェースの多重継承は認められる  
```java
public class クラス名 implements
親インターフェース1, 親インターフェース2, ... {
    ...
}
```
```java
public class PrincessHero
    implement Hero, Princess, Character {
    ...
}
```

### インターフェースの継承
```java
public interface Human extends Creature {
    void talk();
    void watch();
    void hear();
    // さらに親インターフェースからrun()を継承する
}
```

### インターフェースとクラスの同時継承
```java
public class クラス名 extends 親クラス
    implements 親インターフェース1, 親インターフェース2, ... {
    ...
}
```

## 12. 多態性
継承によりis-aの関係が成立しているなら、インスタンスを親クラスの型の変数に代入する事ができる。
- 通常のインスタンスの生成
```java
SuperHero h = new SuperHero();
```
- SuperHeroをざっくりCharacterとして捉える場合
```java
Character C = new SuperHero();
Life lf = new Wizard(); // Lifeはインターフェース
```
※抽象クラスやインターフェースからインスタンスを生み出すことはできないが、型としてりようすることは可能

### 呼び出し可能なメソッド
型のクラスで定義されているメソッド

### 実際に呼び出されるメソッド
インスタンスの型で定義されているメソッド

### 捉え方を変更する方法（キャストの利用）
ダウンキャスト: あいまいな型にはいっている中身を厳密な型に代入する
```java
Character C = new Wizard();
Wizard w = (Wizard)c;
```

### キャストできるかを判定する方法
変数 instanceof 型名
```java
if (c instanceof SuperHero) {
    SuperHero h = (SuperHero)c;
    h.fly();
}
```

### 多様体のメリット
- 複数のインスタンスを同一視して、親クラス型の配列にまとめて扱うことができる。
- 親クラス型の引数や戻り値を利用して、厳密には異なる対象をまとめて処理できる。
- 同一視して取り扱っても、個々のインスタンスは各クラスにおける定義に従い、異なる動作を行う。

## 13. カプセル化
フィールドへの読み書きや、メソッドの呼び出しを制限する機能。
メンバへのアクセス制御の指定方法と範囲

### メンバに対するアクセス制御
|名称 |指定方法 |アクセスを許可する範囲 |
|:---|:---|:---|
|private |private |自分自身のクラス |
|package private |(何も書かない) |自分と同じパッケージに属するクラス |
|protected |protected |自分と同じパッケージに属するか、自分を継承した子クラス |
|public |public |すべてのクラス |

- フィールドのアクセス制御  
  アクセス修飾子 フィールド宣言;
  
- メソッドのアクセス制御  
  アクセス修飾子 メソッド宣言 { ... }

### メンバに関するアクセス修飾の定石
- フィールドは全てprivate
- メソッドは全てpublic

### クラスに対するアクセス制御
|名称 |指定方法 |アクセスを許可する範囲 |
|:---|:---|:---|
|package private|(何も書かない) |自分と同じパッケージに属するクラス |
|public |public |すべてのクラス |

※1 非publicクラスのクラス名はソースファイル名と異なっても良い  
※2 非publicクラスは、1つのソースファイルにクラスを複数宣言して良い  

## 14. Javaを支えるクラス
### java.lang.Objectクラス
あるクラスを定義するときに、extendsで親クラスを指定しなければ、java.lang.Objectクラスを継承したとみなされる。  
java.lang.Objectは下記のようなメソッドを有する。  
- equals()  
  等価であるかどうかを判定する。`h1.equals(h2)`  
  等価の判定方法を変える場合は、オーバーライドする。
  ```java
  public boolean equals(Object O) {
      if (this == o){ return true; }
      else { return false; }
  }
  ```
- toString()  
  クラスの文字列表現を返す。意図する文字列表現にする場合はオーバーライドする。  
  ```java
  public class Hero {
      String name;
      int hp;
      ...
      public String toString() {
          return "名前: " + this.name + "/HP: " + this.hp;
      }
  }
  ```

### 静的フィールド
同じクラスから生成されたインスタンスでフィールドを共有したい場合には、フィールド宣言の先頭にstaticキーワードを追加します。  
1. フィールド変数の実体がクラスに準備される。
2. 全インスタンスに、箱の分身が準備される。
3. インスタンスを1つも生み出さなくてもフィールドが利用可能となる。
- 宣言方法  
  ```java
  public class Hero {
      String name;
      int hp;
      static int money; // 静的フィールド
      ...
  }
  ```  
- アクセス方法  
  ①クラス名.静的フィールド名  
  ②インスタンス変数名.静的フィールド名  

### 静的メソッド
1. メソッド自体がクラスに属するようになる（クラス名を使って呼び出せる）。
2. インスタンスにメソッドの分身が準備される（インスタンスからも呼び出せる）。
3. インスタンスを生み出さなくても呼び出せる。
- 宣言方法  
  ```java
  public class Hero {
      String name;
      int hp;
      static int money;
      ...
      public static void setRandomMoney() {
          Hero.money = (int)(Math.random() * 1000);
      }
  }
  ```
- アクセス方法  
  ①クラス名.メソッド名();  
  ②インスタンス名.メソッド名();  

- 静的メソッドの制約  
  staticのついていない、フィールドやメソッドを参照できない。

### 静的メンバのインポート
```java
import static パッケージ名.クラス名.静的メンバ名;
```

## 15. コレクション
利用方法
1. import文を記述する。
2. <>記号を使って、格納するインスタンスの型を指定する。
3. 宣言時のサイズ指定は不要であり、要素は随時追加できる。
```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> points = new ArrayList<Integer>();
        ...
    }
}
```

ラッパークラス  
コレクションにはインスタンスでないもの（基本データ型）は格納できないため、「基本データ型の情報を中身に保持すること」を責務とする8つのラッパークラスを利用する必要がある。
|基本データ型 |ラッパークラス |
|:---|:---|
|byte |java.lang.Byte |
|short |java.lang.Short |
|int |java.lang.Integer |
|long |java.lang.Long |
|float |java.lang.Float |
|double |java.lang.Double |
|char |java.lang.Char |
|boolean |java.lang.Boolean |

※ Javaにはラッパークラスのインスタンと基本データ型のデータを相互に自動変換する機能が備わっている。

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> points = new ArrayList<Integer>();
        points.add(10); //自動的にIntegerに変換される
        points.add(80);
        points.add(75);
        for (int i : points) { // 拡張forも利用可能
            System.out.println(i);
        }
    }
}
```
### ArrayList
インスタンスを格納できるリスト。
- 宣言  
  ```java
  ArrayList<~> 変数名 = new ArrayList<~>();
  ```
  ※２つ目の<>は省略可能。１つめの<~>を参考にする。

- 要素の格納  
  - 挿入: `add(i, value)`  
  - 上書き: `set(i, value)`  

- 要素の取り出し  
  - `get(i)`

- リストの調査  
  - 要素数: `size()`  
  - 要素数が0かどうか: `isEmpty()`  
  - ある値が含まれるか: `contains(value)`
  - 何番目のいちに含まれるか: `indexOf(value)`

- 要素の削除  
  - すべての要素: `clear()`
  - 指定位置: `remove(i)`

- 拡張forの利用  
  ```java
  for (リスト要素の型 e : リスト変数) {
      /* eで要素を読み書き */
  }
  ```

- イテレータ  
  コレクションクラスの中身を順に取り出すための専用の道具。
  ```java
  Iterator<リスト要素の型> it = リスト変数.iterator();
  while (it.hasNext()) {
      リスト要素の型 e = it.next();
      /* 要素eを用いた処理 */
  }

### LinkedList
- ArrayListと使い方はほとんど同じ、連結リストと呼ばれる構造を応用している。
- ArrayListとLinkedListでは内部構造の違いによる得意・不得意がある。

|ArrayList |比較項目 |LinkedLIst |
|:---:|:---:|:---:|
|配列 |内部構造 |連結リスト |
|☓（遅い） |要素の挿入・削除 |○（速い） |
|○（速い） |指定位置の要素の取得 |☓（遅い） |

### Set
- 重複は許さないが、順番は問わないデータの集まりを利用する場合に用いる。
- HashSet, LinkedHashSet, TreeSetがある。
- LinkedHashSetは、値を格納した順序に整列。
- TreeSetは、自然順序付けで整列（辞書順）。
- 宣言  
  ```java
  Set<~> 変数名 = new HashSet<~>();
  ```

### Map
- キーと値のペアとして格納するデータ構造
- 宣言
  ```java
  Map<キーの型, 値の型> マップ変数 = new HashMap<キーの型, 値の型>();
  ```
  ※ キーの重複は許されない。
- 拡張for
  ```java
  for (キーの型 key : マップ変数.keySet()) {
      値の方 value = マップ変数.get(key);
      /* keyとValueを用いて何らかの処理を行う */
  }
  ```

## 16. 例外
- 例外処理の基本パターン
  ```java
  try {
      通常実行される文
  } catch(例外クラス 変数名) {
      例外発生時に実行される文
  }
  ```
  tryブロック内を実行中に例外的状況が発生したことをJVMが検知すると、処理は直ちにcatchブロックに移行する。

- 二種類以上の例外をcatchするパターン
  ```java
  try {
      通常実行される文
  } catch(例外クラス 変数名) {
      例外発生時に実行される文
  } catch(例外クラス 変数名) {
      例外発生時に実行される文
  }
  ```

- ざっくりと例外をcatchするパターン
  ```java
  try {
      通常実行される文
  } catch(Exception e) {
      例外発生時に実行される文
  }
  ```

- 例外発生の如何を問わず処理を実行
  ```java
  try {
      通常実行される文
  } catch(Exception e) {
      例外発生時に実行される文
  } final {
      例外があってもなくても必ず実行する処理
  }
  ```

- 自動的にclose()が呼ばれるtry-catch文
  ```java
  try (closeによる後片付けが必要な変数の宣言) {
      通常実行される文
  } catch(Exception e) {
      例外発生時に実行される文
  }
  ```
  
- スロー宣言による例外伝搬の許可  
  スロー宣言を行うことで、発生するチェック例外をキャッチせず呼び出し元に伝搬させることが許可される。
  ```java
  public static void subsub() throws ioexception {
      filewriter fw = new filewriter("data.txt");
  }
  ```

- 例外的状況をJVMに報告する
  ```java
  throw 例外インスタンス;
  ```
  例
  ```java
  if (age < 0) {
      throw new IllegalArgumentException("年齢は0以上の数を指定すべきです。")
  }
  ```

- オリジナルの例外クラスの定義  
  定義
  ```java
  public class UnsupportedMusicFileException extends Exception {
      public UnsupportedMusicFileException(String msg) {
          super(msg);
      }
  }
  ```

  利用
  ```java
  public class Main {
      public static void main(String[] args) {
          try {
              // 試験的に例外を発生させる。
              throw new UnsupportedMusicFileException("未対応のファイルです");
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  }
  ```
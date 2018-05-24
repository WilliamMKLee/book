# Coding style

1. 名稱
    1. 變數或是 function 以 boolean 方式存在, 名子開頭請以
        - is
        - can
        - has
        - should
    2. Naming Scalars Like Objects
        ```
        // bad
        store = "Jason's Capsaicin Station"
        // good
        store_name = "Jason's Capsaicin Station"
        ```
        Explanation: If I see a variable name like store, I think it’s an object. This problem becomes especially severe when the codebase does in fact have a class called Store and some stores are instances of that class and some stores are just store names.

    3. Naming Counts Like Collections

        ```
        // bads
        products = 0
        // good
        product_count = 0
        ```

        Explanation: If I see a variable called products I would probably expect its value to be a collection of some sort. I would be surprised when I tried to iterate over the collection only to discover that it’s actually an integer.

    4. Naming a Variable After Its Type

        ```
        // bad
        array = []
        // good
        customers = []
        ```

        Explanation: A variable called array or hash could contain pretty much anything. By choosing a name like this you’re forcing the reader to do all the thinking.

    5. Use of “Stuff Words” For Collections

        Bad examples:

        ```
        news[0]
        inventory[0]
        ```

        Good examples:

        ```
        articles[0]
        inventory_items[0]
        ```
        Explanation: There are certain words that have no singular form. Examples include “stuff”, “garbage” and “laundry”. I call these “stuff words”. This anti-pattern especially applies to database table names.


2. 用介係詞組成變數名稱(of,for,from,on)
    ```
    var daysSinceModification = 3; // 在修改已過了3天
    var workDaysPerWeek = 5; // 每週工作5天
    var daysUntilDeadline = 10; // deadline前還剩10天
    ```
3. 使用更具體的單位
    如等待時間
    ```
    //bad
    waitingOfTimes
    // ok
    waitingOfSeconds
    ```
4. 使用更好的Iterator; 不要使用 i,j,k, 這樣可以提高可讀性, 也比較容易 debug
    如 Key/Value Mystery

    Bad examples:

    ```
    products.each { |key, value| puts value }
    products.each { |k, v| puts v }
    ```

    Good example:

    ```
    products.each { |name, price| puts price }
    ```

    Explanation: Names like key and value have almost no meaning. There’s almost always a more purpose-revealing option.


5. Function Name的prefix都是動詞;
    - fetch：從遠端(透過API)獲取資料，例如：fetchUsers()
    - load：從本地端加載資料，例如：loadFile()
    - calculate/calc：通過計算獲取資料，例如：calcBMI()
    - show：顯示物件，如showModal()、showDialog()
    - remove：將資料之間的關係移除，資料本身還是會存在
    - delete/destroy：將資料刪除，資料將會不存在
    - on：定義event的時候使用，像是onClick,onChange
    - handle：當onClick之類的event發生時所觸發的function，
        例如：handleClick，如果click後面有受詞的話，
        這將受詞移到click前方* 例如：handleButtonClick
    - get/set
    - create: insert append add append
    - edit: modify update
    - complete: finish done end
    - send:   deliver, dispatch, announce, distribute, route
    - find:   search, extract, locate, recover
    - start:  launch, create, begin, open
    - make:   create, set upm build, genernate, compose, add, new

6. 縮寫真的方便但並不是最好; 廣為人知的才能夠用, 如果只有開發團隊懂的縮寫還是少用, 或是有一個對照表

    Bad examples:

    ```
    passwd
    fname
    cust
    o
    ```

    Good examples:

    ```
    password
    first_name
    customer
    order
    ```

    Explanation: Abbreviations like passwd violate the Principle of Least Astonishment. If I know a class has a password attribute I should be able to guess that that attribute is called password. Since passwd is pretty much totally arbitrary, it’s a practically unguessable. Plus, how valuable is it to save two keystrokes?

7. 寫註解
    - 在檔案的最前頭寫上整個程式檔案大致是如何運作的檔案註解
  - 除了解釋程式運作的原理外，還可以描述為什麼要用這樣子的寫法來寫，可能是效能上的需求之類的
  - 使用 TODO FIXME 等註解標籤
    - TODO可以標記尚未製作或是需要優化的部分
    - FIXME是不能運作需要修復的部分
  - 在設定常數的時候給予註解其實也能幫助理解，讓開發者更有概念， 像是下面程式註解說明為什麼要設定為1000的理由
    ```
    // 加上合理的限制 - 沒有人能讀那麼多文章
    const int MAX_RSS_SUBSCRIPTIONS = 1000;
    ```


「英文不好」是個很大的題目，相對於「聽、讀」，「說、寫」的自學門檻較高。
以程式設計師來說，「寫英文」的需求可分為至少兩大方面:

* 命名
    - 名詞: 變數(variable), 類別(class)
    - 動詞: 函式(function)/方法(method)

* 說明/描述
    - 短文註解 (code/commit comment)
    - 長篇文件(documentation)/手冊(manual)

這個 [微軟 PowerShell 指令動詞列表](https://msdn.microsoft.com/en-us/library/ms714428.aspx)當然不是唯一的標準，但它列出了許多動 詞 (尤其是程式設計領域常用的動詞) 及其使用情景的說明，可以作為 動詞命名 的參考。



refer:

- [allenwang15: 程式的命名與coding style討論](https://www.ptt.cc/bbs/Soft_Job/M.1525745915.A.076.html)
- [Jason: Variable Name Anti-Patterns](https://www.codewithjason.com/variable-name-anti-patterns/)
- [AmosYang:  Re: [討論] 註解 用中文還是英文](https://www.ptt.cc/bbs/Soft_Job/M.1521501755.A.411.html)

further reading:

- [How To Write Unmaintainable Code](https://github.com/Droogans/unmaintainable-code)

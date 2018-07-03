# 關於反覆器模式  

我們嘗試建立一個簡易版的鏈結串列。

## 設計一個列表類別

先建立一個節點類別:

``` C#
public class SimpleNode
{
    public string NodeName { get; set; }
    public SimpleNode Next { get; set; }
    
    public SimpleNode(string name)
    {
        NodeName = name;
    }
}
```

以及一個串列類別:

``` C#
public class SimpleList
{
    public SimpleNode Root { get; set; }
    public SimpleNode Last { get; set; }
    
    public void AddNode(SimpleNode node)
    {
        if (Root == null)
        {
            Root = node;
            Last = Root;
        }
        else
        {
            Last.Next = node;
            Last = Last.Next;
        }
    }
}
```

然後，我們就可以建立一個簡單的列表，並且印出所有節點內容:

``` C#
var list = new SimpleList();
list.AddNode(new SimpleNode("node1"));
list.AddNode(new SimpleNode("node2"));
list.AddNode(new SimpleNode("node3"));

var current = list.Root;
while (current != null)
{
    Console.Write(current.NodeName);
    current = current.Next;
}
// Output: node1node2node3
```

但是，這樣的操作行為會暴露出資料結構，如果內部換成陣列，所有的操作方法都必須改變，因此我們必須將目前的行為抽象化，這就是反覆器模式。

## 使用反覆器模式

先建立一個反覆器介面，加入拜訪節點的行為介面:

``` C#
public interface Iterator
{
    bool HasNext();
    SimpleNode Next();
}
```

再來我們建立第二代類別 SimpleList2，繼承 SimpleList，加入一些屬性，並且實作 Iterator 介面:

``` C#
public class SimpleList2 : SimpleList, Iterator
{
    public SimpleNode Current { get; set; }
    public bool IsDoing { get; set; }

    public SimpleList2()
    {
        IsDoing = false;
    }

    public bool HasNext()
    {
        if (IsDoing)
        {
            Current = Current.Next;
        }
        else
        {
            Current = Root;
            IsDoing = true;
        }

        IsDoing = Current != null;
        return IsDoing;
    }

    public SimpleNode Next()
    {
        return Current;
    }
}
```

然後，我們一樣建立一個列表，並且印出所有節點內容:

``` C#
var list = new SimpleList2();
list.AddNode(new SimpleNode("node1"));
list.AddNode(new SimpleNode("node2"));
list.AddNode(new SimpleNode("node3"));

Iterator iterator = list;
while (iterator.HasNext())
{
    var node = iterator.Next();
    Console.Write(node.NodeName);
}
// Output: node1node2node3
```

這樣一來，我們就可以使用抽象的行為來拜訪列表節點，客戶端程式不必考慮複雜的資料結構，只要知道行為就好了，這就是設計模式中的反覆器模式。現在的高階程式語言都有已經有實作在集合類別中，像是 C# 的集合物件都可以用 foreach 語法進行拜訪，這就是反覆器模式的威力。

不過，在上面的例子，我們設計的集合類別還無法使用 foreach 語法，是因為沒有實作 GetEnumerator 方法，所以我們再來做一些修改。

## 讓自己的列表適用 foreach 語法

我們先建立第三代類別 SimpleList3，一樣是繼承 SimpleList，然後和 SimpleList2 不同的是，這裡只寫一個方法  GetEnumerator，建立並且回傳一個 Enumerator 物件:

``` C#
public class SimpleList3 : SimpleList
{
    public IEnumerator<SimpleNode> GetEnumerator()
    {
        IEnumerator<SimpleNode> enumerator = new SimpleEnumerator(Root);
        return enumerator; 
    }
}
```

然後，我們建立一個 SimpleEnumerator 類別，必須實作 IEnumerator 介面:

``` C#
public class SimpleEnumerator : IEnumerator<SimpleNode>
{
    public SimpleEnumerator(SimpleNode root)
    {
        Root = root;
        IsDoing = false;
    }

    public SimpleNode Root { get; set; }
    public SimpleNode Current { get; set; }
    public bool IsDoing { get; set; }

    object IEnumerator.Current
    {
        get
        {
            return Current;
        }
    }

    public void Dispose()
    {
        Root = null;
        Current = null;
    }

    public bool MoveNext()
    {
        if (IsDoing)
        {
            Current = Current.Next;
        }
        else
        {
            Current = Root;
            IsDoing = true;
        }

        IsDoing = Current != null;
        return IsDoing;
    }

    public void Reset()
    {
        IsDoing = false;
    }
}
```

然後，我們再次建立列表物件，並使用 foreach 語法拜訪列表節點:

``` C#
var list = new SimpleList3();
list.AddNode(new SimpleNode("node1"));
list.AddNode(new SimpleNode("node2"));
list.AddNode(new SimpleNode("node3"));

foreach (var node in list)
{
    Console.Write(node.NodeName);
}
// Output: node1node2node3
```

## 結論

雖然高階程式語言都已經實作反覆器模式，但是對於程序員來說，了解其中原理仍然是非常重要的。


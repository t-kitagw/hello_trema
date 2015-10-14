レポート課題
===========


## 課題

HelloTrema (`./lib/hello_trema.rb`)  を改造して次の 2 つの機能を実装しよう。

### その1

スイッチを停止したら次のメッセージを表示するようにしてみよう:

```
Bye 0xabc
```

* ヒント: [スイッチの停止方法](https://relishapp.com/trema/trema/docs/handlers/switch-disconnected-handler)

### その2

HelloTrema が起動したら次のメッセージを表示するようにしてみよう:

```
HelloTrema started.
```

ただし、次の回答ではダメ (なぜダメか？も考えよう)

```ruby
class HelloTrema < Trema::Controller
  def start(_args)
    logger.info 'HelloTrema started.'
  end
  ...
```

* ヒント 1: [Object#class メソッド](http://ruby-doc.org/core-2.0.0/Object.html#method-i-class)
* ヒント 2: [Module#name メソッド](http://ruby-doc.org/core-2.0.0/Module.html#method-i-name)

## 回答

```
# Hello World!
class HelloTrema < Trema::Controller
  def start(_args)
    logger.info self.class.name + ' started.'
  end

  def switch_ready(datapath_id)
    logger.info "Hello #{datapath_id.to_hex}!"
  end

  def switch_disconnected(datapath_id)
    logger.info "Bye #{datapath_id.to_hex}"
  end
end
```

```
self.class.name
```
自身のクラスを呼び、そのクラスの名前を呼ぶことで、自クラス名を表示する。（課題その2）

```
def switch_disconnected(datapath_id)
```
切断時に呼ばれるメソッド。"Bye (呼び出し元のid)"と表示する。（課題その1）
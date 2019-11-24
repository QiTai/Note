### Chain of Responsibility
```cpp
class HelpHandler {
public:
    HelperHandler(HelpHandler *s) : _successor(s) { }
    virtual void HandleHelp();
private:
    HelpHandler* _successor;
}；

void HelpHandler::HandleHelp() {
    if (_successor) {
        _successor->HandleHelp();
    }
}
// 分派函数的框架
void Handler::HandlerRequest (Request *theRequest) {
  switch (theRequest->GetKind()) {
  case Help:
    HandleHelp((HelpRequest*) theRequest);
    break;
  case Print:
    HandlePrint((PrintRequest*) theRequest);
    break;
  default:
    // ...
    break;
  }
}
// 子类只处理自己感兴趣的请求
class ExtendedHandler : public Handler {
public:
  virtual void HandleRequest(Request* theRequest);
}
void ExtendedHandler::HandlerRequest (Request* theRequest) {
  switch (theRequest->GetKind()) {
  case Preview:
    // ...
    break;
  default:
    // ...
    break;
  }
}
```

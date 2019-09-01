# PortWallet iOS(swift) SDK

The PortWallet iOS SDK makes it quick and easy to build an excellent payment experience in your iOS app. We provide powerful and customizable UI screens and elements.

# Requirements
* iOS 10.0+
* Xcode 9.0+
* Swift 4.0+

# Usage

Import the SDK
```
import PortWallet
```
init portwallet SDK
```
let portwallet = Portwallet(appKey: String, secretkey: String, env: Environment, theme: PortWalletTheme)
```
or
```
// with default theme
let portwallet = PortWallet(appKey: String, secretkey: String, env: Environment)
```

change environmant
```
portwallet.setEnv(env: .sandbox)
portwallet.setEnv(env: .production)
```

## Portwallet Theme
Customize UI with `PortWalletTheme` class. i.e
```
let theme = PortWalletTheme(
    buttonBackgroundColor: UIColor,
    buttonTextColor: UIColor,
    iconTintColor: UIColor,
    textFieldTintColor: UIColor,
    navBackgroundColor: UIColor,
    navTintColor: UIColor
)
```

## Payment Method
```
- anonymousPay
- pay
- login
- logout
- manageAccount
```

### anonymous pay
Customer able to pay without login.
```
// Params
- viewController: UIViewController
- invoice: [String: Any]

// example
portwallet.anonymousPay(viewController: self, invoice: invoice)

```

### login
Able to login using `login` method.
```
// Params
- viewController: UIViewController

// Return
- token in delegate method

// example
portwallet.login(viewController: self)
```

### logout
Logout from user account
```
// Params
- viewController: UIViewController
- token: String


// example
portwallet.logout(viewController: self, token: String)
```

### pay
Pay with login account
```
// Params
- viewController: UIViewController
- token: String
- invoice: [String: Any]

// example
portWallet.pay(viewController: UIViewController, token: String, invoice: [String: Any])
```

### manage account
Manage portwallet user account
```
// Params
- viewController: UIViewController
- token: String

// example
portWallet.manageAccount(viewController: UIViewController, token: String)
```

## Delegate Methods
There are three delegate methods in `Portwallet`.
```
- getSecret
- success
- failure
```

Example
```
extention ViewController: PortWalletDelegate {
    func getSecret() { // return MD5 hash of secretKey and timestamp
        return ...
    }

    func success(response: Dictornary<String, Any>) {
        ....
    }

    func failur(response: Dictonary<String, Any>) {
        ...
    }
}
```
All success/failur message send to delegate methods.
### Response
Success

```
// Structure
{
    "success": True,
    "method": String (enum),
    "data": [String: Any]
}
```

Failur
```
// Structure
{
    "success": False,
    "method": String (enum)
    "error": {
        "code": Int,
        "message": String,
        "Description": String
    }
}
```

Response Method Type:
```
// Enum: PWMethodType
- login
- logout
- pay
- anonymousPay
- manageAccount
```

### Error Code
- `4005xxx`: Any type of network error
- `4002xxx`: Invoice validation error
- `400100x`: Token or Secret key empty
- `400101x`: Logout Error
- `4004xxx`: Invoice create error
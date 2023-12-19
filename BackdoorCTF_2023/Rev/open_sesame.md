### Open Sesame

Using jadx `jadx -d . open_sesame.apk` or your favorite decompiler, we get the following under sources/com/example/opensesame: -

```java
package com.example.open_sesame;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.app.AppCompatDelegate;

public class MainActivity extends AppCompatActivity {
    private static final int[] valid_password = {52, AppCompatDelegate.FEATURE_SUPPORT_ACTION_BAR, 49, 98, 97, 98, 97};
    private static final String valid_user = "Jack Ma";
    private Button buttonLogin;
    private EditText editTextPassword;
    private EditText editTextUsername;

    /* access modifiers changed from: protected */
    public void onCreate(Bundle bundle) {
        super.onCreate(bundle);
        setContentView(R.layout.activity_main);
        this.editTextUsername = (EditText) findViewById(R.id.editTextUsername);
        this.editTextPassword = (EditText) findViewById(R.id.editTextPassword);
        Button button = (Button) findViewById(R.id.buttonLogin);
        this.buttonLogin = button;
        button.setOnClickListener(new View.OnClickListener() {
            public void onClick(View view) {
                MainActivity.this.validateCredentials();
            }
        });
    }

    /* access modifiers changed from: private */
    public void validateCredentials() {
        String trim = this.editTextUsername.getText().toString().trim();
        String trim2 = this.editTextPassword.getText().toString().trim();
        if (!trim.equals(valid_user) || !n4ut1lus(trim2)) {
            showToast("Invalid credentials. Please try again.");
            return;
        }
        "flag{" + flag(Integer.toString(sl4y3r(sh4dy(trim2))), "U|]rURuoU^PoR_FDMo@X]uBUg") + "}";
    }

    private boolean n4ut1lus(String str) {
        int[] it4chi = it4chi(str);
        if (it4chi.length != valid_password.length) {
            return false;
        }
        for (int i = 0; i < it4chi.length; i++) {
            if (it4chi[i] != valid_password[i]) {
                return false;
            }
        }
        return true;
    }

    private int[] it4chi(String str) {
        int[] iArr = new int[str.length()];
        for (int i = 0; i < str.length(); i++) {
            iArr[i] = str.charAt(i);
        }
        return iArr;
    }

    private String sh4dy(String str) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < str.length(); i++) {
            char charAt = str.charAt(i);
            if (Character.isDigit(charAt)) {
                sb.append(charAt);
            }
        }
        return sb.toString();
    }

    private int sl4y3r(String str) {
        return Integer.parseInt(str) - 1;
    }

    private String flag(String str, String str2) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < str2.length(); i++) {
            sb.append((char) (str2.charAt(i) ^ str.charAt(i % str.length())));
        }
        return sb.toString();
    }

    private void showToast(String str) {
        Toast.makeText(this, str, 0).show();
    }
}
```

Reading up through the code, I created a python script to get the flag: -

```py
a = "40"
b = "U|]rURuoU^PoR_FDMo@X]uBUg"
c = []
for i in range(len(b)):
	c.append(chr(ord(b[i])^ord(a[i%len(a)])))
print(c)
print(''.join(x for x in c))
```

```
$ python3 solve-open-sesame.py
['a', 'L', 'i', 'B', 'a', 'b', 'A', '_', 'a', 'n', 'd', '_', 'f', 'o', 'r', 't', 'y', '_', 't', 'h', 'i', 'E', 'v', 'e', 'S']
aLiBabA_and_forty_thiEveS
```

### Flag

`flag{aLiBabA_and_forty_thiEveS}`

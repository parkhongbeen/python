## Django form Login

### 1. 로그인 예외처리

```python
<form.py>
class LoginForm(forms.Form):
    username = forms.CharField(
        error_messages={
            'required': '아이디를 입력해주세요.'
        },
        max_length=32, label="사용자이름"
    )
    password = forms.CharField(
        error_messages={
            'required': '비밀번호를 입력해주세요.'
        },
        widget=forms.PasswordInput, label='비밀번호'
    )

    def clean(self):
        cleaned_data = super().clean()
        username = cleaned_data.get('username')
        password = cleaned_data.get('password')

        if username and password:
            try:																					#1
                user = User.objects.get(username=username)
                if not check_password(password, user.password):
                    self.add_error('password', '비밀번호를 틀렸습니다.')
                else:
                    self.user_id = user.id
            except Exception:															#2
                self.add_error('username', '존재하지 않는 아이디입니다.')
```

1) 예외가 발생할 수 있는 문장입니다.

2) 예외가 발생한 경우, form의 error필드에 데이터를 삽입할 수 있습니다.

### 2. 404페이지로 redirect

```python
from django.http import Http404

try:
  board = Board.objects.get(pk=pk)
except Board.DoesNotExist:
  raise Http404('페이지를 찾을 수 없습니다.')     #1
```

1) raise Http404('보여줄 메시지')를 사용하여 404페이지로 redirect 시킬 수 있습니다.


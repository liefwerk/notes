# Updating the user profile

How can we allow the user to update it's own profile ?

## Updating the Profile

First, we'll have to add some forms.
In `forms.py` we add this snippet of code

```py
from django import forms
from django.contrib.auth.models import User
from django.contrib.auth.forms import UserCreationForm
from .models import Profile

class UserRegisterForm(UserCreationForm):
  email = forms.EmailField()
  
  class Meta:
    model = User
    fields = ['username', 'email', 'password1', 'password2']

class UserUpdateForm(forms.ModelForm):
  email = forms.EmailField()

  class Meta:
    model = User
    fields = ['username', 'email']

class ProfileUpdateForm(forms.ModeForm):
  class Meta:
    model = Profile
    fielfs = ['image']
```

Then we register those forms in our `views.py` file

```py
from .forms import UserRegisterForm, UserUpdateForm, ProfileUpdateForm

@login_required
def profile(request):
  if request.method == 'POST':
    u_form = UserUpdateForm(request.POST, instance=request.user)
    p_form = ProfileUpdateForm(request.POST,
                               request.FILES,
                               instance=request.user.profile)
    if u_form.is_valid() and p_form.is_valid():
      u_form.save()
      p_form.save()
      messages.success(request, f'Your account has been updated.')
      return redirect('profile')
  else:
    u_form = UserUpdateForm(instance=request.user)
    p_form = ProfileUpdateForm(instance=request.user.profile)  
  
  context = {
    'u_form': u_form,
    'p_form': p_form
  }
  
  return render(request, 'users/profile.html', context)
```

Finally, we can add our form to the form.html template

```django
<form method="POST" enctype="multipart/form-data">
  {% csrf_token %}
  <fieldset class="form-group">
    <legend class="border-bottom mb-4">Profile Info</legend>
    {{ u_form|crispy }}
    {{ p_form|crispy }}
  </fieldset>
  <div class="form-group">
    <button class="btn btn-outline-info" type="submit">Update</button>
  </div>
</form>
```

## Resizing the Profile image

This is an easy solution on how to automatically resize the profile image when it is updated.
We'll have to update our Profile method and add our own save function.

```py
from PIL import Image

class Profile(models.Model):
  user = models.OneToOneField(User, on_delete=models.CASCADE)
  image = models.ImageField(default='default.jpg', upload_to='profile_pics')

  def __str__(self):
    return f'{self.user.username} Profile'

  # our new save function  
  def save(self):
    super().save()

    # here we get the updated image
    img = Image.open(self.image.path)

    # an if statement to resize it
    if img.height > 300 or img.width > 300:
      output_size = (300, 300)
      img.thumbnail(output_size)
      img.save(self.image.path)
```

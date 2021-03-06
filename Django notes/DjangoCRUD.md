# Building CRUD using Django:

After building the database (The model):

## Create:
1. Building the Template:
   in templates folder -> create.html
   ```
   {%block content%}
   <form action="" method="post">
      {% csrf_token%} # for security purposes
     {{form.as_p}} # this will create each input from the table
   <input type="submit">
   {%endblock content%}
   ```
2. Building the view:
   in app folder -> views.py:
   ```
   class CreateView(CreateView):
     model = modelName
     template_name = 'create.html'
     fields = ['subject', 'body', 'author'] // what I need in the form
   ```

3. Adding the URL:
   In app folder -> urls.py:
    ```
    urlpatterns =[
        path(''create/, CreateView.as_view(), name='create)
    ]
    ```

4. Add redirect URL when I click submit:
   In app folder -> models.py -> in the model class:
   ```
   from django.urls import reverse
   def get_absolute_url(self):
     return reverse('template_name', args=[str(self.pk)])
   ```

## Update:
1. Building the Template:
   * in templates folder -> update.html
   ```
   {%block content%}
   <form action="" method="post">
      {% csrf_token%} # for security purposes
     {{form.as_p}} # this will create each input from the table
   <input type="submit">
   {%endblock content%}
   ```
   * in template folder -> details.html:
  ```
  <a href="{url 'update' post.pk}"> Update <a>
  ```
2. Building the view:
   in app folder -> views.py:
   ```
   class UpdateView(UpdateView):
     model = modelName
     template_name = 'Update.html'
     fields = ['subject', 'body', 'author'] // what I need in the form
   ```

3. Adding the URL:
   In app folder -> urls.py:
    ```
    urlpatterns =[
        path('update/<int:pk>', UpdateView.as_view(), name='update)
    ]
    ```

4. Add redirect URL when I click submit:
   In app folder -> models.py -> in the model class:
   ```
   from django.urls import reverse
   def get_absolute_url(self):
     return reverse('template_name', args=[str(self.pk)])
   ```

## Delete:
1. Building the Template:
   * in templates folder -> delete.html
   ```
   {%block content%}
      <p> Are you sure you want to delete {{post.subject}} </p>

       <form action="" method="post">
       {% csrf_token%}
       <input type="submit">

   {%endblock content%}
   ```
   * in template folder -> details.html:
  ```
  <a href="{url 'delete' post.pk}"> delete <a>
  ```
2. Building the view:
   in app folder -> views.py:
   ```
   from django.urls import reverse_lazy
   class DeleteView(DeleteView):
     model = modelName
     template_name = 'delete.html'
     success_url = reverse_lazy('list')

   ```

3. Adding the URL:
   In app folder -> urls.py:
    ```
    urlpatterns =[
        path('delete/<int:pk>', DeleteView.as_view(), name='delete)
    ]
    ```
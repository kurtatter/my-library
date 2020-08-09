## InstaPy

#### Лайки

Этот метод используется, только когда активен метод ``` interact_by_... ```

По умолчаться посты будут лайкаться при использовании ```like_by_...``` 

```python
# ~70% of the by InstaPy viewed posts will be liked

session.set_do_like(enabled=True, percentage=70)
```



#### Комментирование

```python
# default enabled=False, ~ every 4th image will be commented on

session.set_do_comment(enabled=True, percentage=25)
session.set_comments(['Awesome', 'Really Cool', 'I like your stuff'])

# you can also set comments for specific media types (Photo / Video)

session.set_comments(['Nice shot!'], media='Photo')
session.set_comments(['Great Video!'], media='Video')

# and you can add the username of the poster to the comment by using

session.set_comments(['Nice shot! @{}'], media='Photo')
```


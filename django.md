# Django

## Getting Started

```bash
pip install -r requirements.txt
./manage.py makemigrations
./manage.py migrate
./manage.py createsuperuser
./manage.py runserver
```

## Bootstrap Forms

**Add class in field defintion**

```python
class ProjectFilterForm(forms.Form):

    technology = forms.ModelMultipleChoiceField(
        label='Technology',
        required=False,
        queryset=Technology.objects,
        to_field_name='slug',
        widget=forms.SelectMultiple(attrs={'class': 'form-control'}),
    )
```

**Add class by looping fields**

```python
class ProjectFilterForm(forms.Form):

    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)

        for field in self:
            field.field.widget.attrs['class'] = 'form-control'
```

**Add class by template system**

*TBD*

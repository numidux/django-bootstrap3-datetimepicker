About
=====

This a fork of https://github.com/nkunihiko/django-bootstrap3-datetimepicker
The original repo is out of date and does not support django 1.11 so I forked and merged a pull request (#65)


django-bootstrap3-datetimepicker
================================

This package uses Bootstrap v3 datetimepicker widget version 2 provided by the following project:
 https://github.com/Eonasdan/bootstrap-datetimepicker

The correct formatting options for dates can be found here:
 http://momentjs.com/docs/

It works only with Bootstrap3. If you are using Bootstrap2 in your Django project, 
visit https://github.com/zokis/django-bootstrap-datetimepicker


Install
-------------------------------

* Run `pip install git+https://github.com/numidux/django-bootstrap3-datetimepicker`
* Add `'bootstrap3_datetime'` to your `INSTALLED_APPS`


Example
--------------------------------

###### forms.py
	from bootstrap3_datetime.widgets import DateTimePicker
	from django import forms
	
    class ToDoForm(forms.Form):
        todo = forms.CharField(
            widget=forms.TextInput(attrs={"class": "form-control"}))
        date = forms.DateField(
            widget=DateTimePicker(options={"format": "YYYY-MM-DD",
                                           "pickTime": False}))
        reminder = forms.DateTimeField(
            required=False,
            widget=DateTimePicker(options={"format": "YYYY-MM-DD HH:mm",
                                           "pickSeconds": False}))

The `options` will be passed to the JavaScript datetimepicker instance. 
Available `options` are explained in the following documents:

* http://eonasdan.github.io/bootstrap-datetimepicker/

You don't need to set the `language` option, 
because it will be set the current language of the thread automatically.

###### template.html
	<!DOCTYPE html>
	<html>
	    <head>
	        <link rel="stylesheet" 
	              href="//netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.css">
	        <link rel="stylesheet" 
	              href="//netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap-theme.css">
	        <script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.js">
	        </script>
	        <script src="//netdna.bootstrapcdn.com/bootstrap/3.0.0/js/bootstrap.js">
	        </script>
	        {{ form.media }}
	    </head>
	    <body>
	        <form method="post" role="form">
	            {% for field in form.visible_fields %}
	            <div id="div_{{ field.html_name }}" 
	                 class="form-group{% if field.errors %} has-error{% endif %}">
	                {{ field.label_tag }}
	                {{ field }}
	                <div class="text-muted pull-right">
	                    <small>{{ field.help_text }}</small>
	                </div>
	                <div class="help-block">
	                    {{ field.errors }}
	                </div>
	            </div>
	            {% endfor %}
	            {% for hidden in form.hidden_fields %}
	                {{ hidden }}
	            {% endfor %}
	            {% csrf_token %}
	            <div class="form-group">
	                <input type="submit" value="Submit" class="btn btn-primary" />
	            </div>
	        </form>
	    </body>
	</html>

Bootstrap3 and jQuery have to be included along with `{{ form.media }}`

Requirements
-------------------------------

* Python >= 2.4
* Django >= 1.3
* Bootstrap >= 3.0



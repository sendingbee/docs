There are various ways how you can grow your audience. You can create your
own HTML forms and add new contacts via the [API](/api/contacts.md). That's
the most flexible way but it also requires work on your part.

An alternative is to use Signup forms. You create these forms from the admin
interface as usual and then you're given an HTML snippet to put on your
website. No additional steps needed.

To make sure you're given an explicit consent to send contacts emails, they
will receive a confirmation email right after they sign up. The process is
called **double opt-in**. Besides preventing abuse, it will also verify that
the given email is actually valid before you send any emails to it.

<p class="centered">
  ![hooks](../_assets/images/signup_forms.png ':size=300')
</p>

### Setup

Select "Signup Forms" in the left sidebar and click New on the right. If you
don't already have a **public** list, it will prompt you to create one. When
a list is **public**, it means it will be visible to your contacts - they
will know they are assigned to that list on their preference page.

<p class="centered">
  ![hooks](../_assets/images/signup_forms2.png)
</p>

As you fill in the details, you will see them previewed immediately on the
right.

##### Terms and Conditions

To be compliant with various regulations, GDPR among others, you need to
provide information about how you're going to use the gathered data. You can
either provide a link to a website where you host the terms yourself or you
can provide them straight in the box.

<p class="centered">
  ![hooks](../_assets/images/signup_forms3.png ':size=500')
</p>

If you provide both the URL and the inline text, the text will have a
preference.

##### Look and feel

By default all signup forms come with a default style (CSS). You can the
background, text color and the same for the Signup button. If you want to
customize the form further, you can override any style with your own CSS. As
in the previous section, you have the option to use an URL or specify the
styles inline in the box.

If you want to start from scratch with no styles included, you can switch the
"Include default CSS?" switch.

<p class="centered">
  ![hooks](../_assets/images/signup_forms4.png)
</p>

##### Additional custom fields

By default there's an input for email only but you can of course add any
number of additional custom fields. For each custom field you can specify a
custom placeholder and also whether the field is required or not.

<p class="centered">
  ![hooks](../_assets/images/signup_forms5.png)
</p>

##### Lists

When somebody submits the form, SendingBee needs to know to which lists they
should be added. In this case, the entire form represents a sign up to a
monthly newsletter. That's why the "Newsletter" list is selected as
implicit.

**Implicit** in this case means contacts are added to the list automatically
when the form is submitted. It's also possible to offer **optional**
subscriptions. Here, we're offering a subscription to the "Weekly highlights"
list. It's optional and so the user needs to explicitly check the box to
subscribe.

<p class="centered">
  ![hooks](../_assets/images/signup_forms6.png)
</p>

You can of course make a form where all of the lists are optional a create a
generic signup widget. The form will enforce that at least one list is
selected.

<p class="centered">
  ![hooks](../_assets/images/signup_forms7.png)
</p>

##### Embed code

As soon as you save the form, you will be given an HTML code (you can also
see the code when you "Edit" the Sign up form). You need to paste this HTML
into your website where you want the Signup form appear.

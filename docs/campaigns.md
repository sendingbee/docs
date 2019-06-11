Now that you have your contacts organized, AWS SES, and delivery providers
set up, it's time to finally send some emails! Navigate to *Campaigns* in the
sidebar and let's get started.

A **campaign** represents a single email sent to recipients. Once a campaign
is sent, it will be delivered as soon as possible to all the matching
contacts at the time. There will also be real time display of the campaign's
performance.

<p class="centered">
  ![campaigns](../_assets/images/campaigns.png)
</p>

#### Continuous campaigns

A campaign can also be **continuous**. A continuous campaign is very similar to
a regular campaign but the campaign gets sent repeatedly every hour until
canceled. Every recipient will still receive the email only once but because
it's sent repeatedly, it's automatically sent to newly matching contacts as they
are added. You can use this to e.g. welcome new contacts to your newsletter.

<p class="centered">
  ![campaigns3](../_assets/images/campaigns3.png ':size=400')
</p>

#### Recipients

**Recipients** are selected using lists and/or segments. You can even specify
multiple lists/segments at the same time and the email will be delivered to
all matching contacts. It's okay if a contact matches more than one selected
list/segment, they will receive the email only once.

<p class="centered">
  ![campaigns2](../_assets/images/campaigns2.png ':size=400')
</p>

#### Email editor

To create the actual **email content**, there's a "what you see is what you
get" (WYSIWYG) editor with predefined widgets that you can drag onto the free
template space. Each component can be further customized by clicking on it.

<p class="centered">
  ![campaigns4](../_assets/images/campaigns4.png ':size=400')
</p>

There are two variants to every email - its **HTML** and **text** versions.
The WYSIWYG editor will automatically create the HTML version. There's no
need to create the text version, SendingBee will automatically convert the
HTML version into plain text. You can of course provide your own text version
in which case it will be used instead.

<p class="centered">
  ![campaigns5](../_assets/images/campaigns5.png ':size=400')
</p>

Templates can use "tags" to include details about a specific contact. You can
choose to address a contact by their name, include details about their
shopping history and more. All of the custom fields assigned to a contact are
available. We will talk more about tags specifically in the
[Templates](/templates.md) section.

<p class="centered">
  ![campaigns11](../_assets/images/campaigns11.png)
</p>

To make creating these highly custom templates easier, SendingBee allows to
preview the template in the context of a contact. Just search for the contact
and the template will be rendered as if received by that specific contact.

<p class="centered">
  ![campaigns9](../_assets/images/campaigns9.png ':size=400')
</p>
<p class="centered">
  ![campaigns10](../_assets/images/campaigns10.png ':size=250')
</p>

Further, by clicking on the envelope icon, SendingBee will send an email with
the current content rendered for the specific contact to your registration
email address (not to the contact).

Many people open emails on their mobile devices. As such, it's important to
make sure your email looks great even when viewed on a smaller screen. To
help with that, you can toggle between previews in Desktop and Mobile modes
with just single click.

<p class="centered">
  ![campaigns12](../_assets/images/campaigns12.png ':size=200')
</p>

#### Cancel and delete

What happens when you accidentally send a campaign? SendingBee allows you to
cancel the sending process at any time. No further emails will be sent. You
can also delete a campaign. If the campaign is currently sending, it will
cancel it and then delete it.

Continue to [Templates](/templates.md).

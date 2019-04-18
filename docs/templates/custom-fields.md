Every contact has a few [Custom fields](/contacts/custom-fields) associated
with it by default (and of course you can add your own). They can be used in
various ways but one particular important is to use them in templates.

##### Output custom fields

You can use custom fields to make emails more personal by for example
including the contact's name. To do that, create a text component and enter
the following as the text:

```
Hello {{ first_name }} {{ last_name }}!
```

In fact, as you might have noticed, when you type `{{` within the text
component's text, a dropdown will show up with the available options.

<p class="centered">
  ![custom-fields1](../_assets/images/templates_custom_fields1.png ':size=400')
</p>

The editor itself will show the raw value as entered.

<p class="centered">
  ![custom-fields](../_assets/images/templates_custom_fields.png ':size=400')
</p>

It's often more convenient to create these templates within a context of a
particular contact. To do that, search for a contact in the upper **Preview
as** box.

<p class="centered">
<p class="centered">
  ![custom-fields2](../_assets/images/templates_custom_fields2.png ':size=400')
</p>
</p>

As soon as a contact is selected, the editor will render the template as if
viewed by the contact. If you want to go back to rendering the template as
written without interpreting of the tags, clear the "Preview as" field using
the cross within the field.

<p class="centered">
<p class="centered">
  ![custom-fields3](../_assets/images/templates_custom_fields3.png ':size=300')
</p>
</p>

##### Transformations

The editor can also transform the value of a custom field before it's
printed. The following transformations are available (note the usage of a
string instead of a custom field for illustrative purposes).

<table>
  <thead>
    <th>
      Expression
    </th>
    <th>
      Result
    </th>
  </thead>

  <tbody>
    <tr>
      <td>
        Hello {{ "" | **default: "world" ** }}
      </td>
      <td>
        Hello world
      </td>
    </tr>
    <tr>
      <td>
        {{ "hello world" | **upcase** }}
      </td>
      <td>
        HELLO WORLD
      </td>
    </tr>
    <tr>
      <td>
        {{ "hEllO WoRld" | **downcase** }}
      </td>
      <td>
        hello world
      </td>
    </tr>
    <tr>
      <td>
        {{ "Hello" | **append:** " World" }}
      </td>
      <td>
        Hello World
      </td>
    </tr>
    <tr>
      <td>
        {{ "World" | **prepend:** "Hello " }}
      </td>
      <td>
        Hello World
      </td>
    </tr>
    <tr>
      <td>
        {{ "hello world" | **capitalize** }}
      </td>
      <td>
        Hello world
      </td>
    </tr>
    <tr>
      <td>
        {{ "Hello\nworld" | **newline_to_br** }}
      </td>
      <td>
        Hello &lt;br /&gt;world
      </td>
    </tr>
    <tr>
      <td>
        {{ "&lt;strong&gt;Hello world&lt;/strong&gt;" | **unescape** }}
      </td>
      <td>
        <strong>Hello world</strong>
      </td>
    </tr>
  </tbody>
</table>

##### Conditions

Sometimes you want to show some content but only if the contact satisfies
certain criteria. For example, you might want to change the title if it's an
existing customer or not.

<p class="centered">
  ![custom-fields5](../_assets/images/templates_custom_fields5.png ':size=400')
</p>

An alternative is to condition entire blocks. Notice that each block has a
**Show If** property.

<p class="centered">
  ![custom-fields4](../_assets/images/templates_custom_fields4.png ':size=400')
</p>

The available operators are **==**, **!=**, **>**, **>=**, **<**, **>=**. For
string custom fields, you can use **contains**. If you want to display the
value for truthy values, you can omit the operator part and leave just the
name of the field.

The following are all valid conditions:

<table>
  <thead>
    <th>
      Condition
    </th>
    <th>
      Description
    </th>
  </thead>

  <tbody>
    <tr>
      <td>
        has_bought_items
      </td>
      <td>
        Evaluates to true if the value is "truthy" (true values, non empty strings, numbers).
      </td>
    </tr>
    <tr>
      <td>
        has_bought_items == true
      </td>
      <td>
        Evaluates to true if the custom field is set to value `true`.
      </td>
    </tr>
    <tr>
      <td>
        first_name == "Jiri" && has_bought_items == true
      </td>
      <td>
        Evaluates to true if the custom field `first_name` is equal to "Jiri" and `has_bought_items` is true at the same time.
      </td>
    </tr>
    <tr>
      <td>
        first_name == "Jiri" || first_name == "Jan"
      </td>
      <td>
        Evaluates to true if the custom field `first_name` is equal to "Jiri" or "Jan".
      </td>
    </tr>
  </tbody>
</table>

Continue to [Meta variables](/templates/meta-variables.md).

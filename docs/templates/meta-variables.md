Besides variables containing custom fields, the editor has also access to a
special set of variables, so called meta variables. There variables are not
connected to contacts but rather to the overall environment.

We will expand the list of supported variables as we go. If you have a need for
a specific variable, please contact us at
[support@sendingbee.com](mailto:suppport@sendingbee.com).

## meta.now

The `meta.now` variable contains the current time in the project's time
zone. It's often used in emails' footers to display the current year.

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
        {{ meta.now }}
      </td>
      <td>
        Tuesday, January 8th 2019, 8:56:28 AM CST
      </td>
    </tr>

    <tr>
      <td>
        {{ meta.now | date: "dddd, MMMM Do YYYY, h:mm:ss A z" }}
      </td>
      <td>
        Tuesday, January 8th 2019, 8:56:28 AM CST
      </td>
    </tr>

    <tr>
      <td>
        {{ meta.now | date: "MMMM DD, YYYY hh:mm:ss" }}
      </td>
      <td>
        January 08, 2019 08:56:28
      </td>
    </tr>
    <tr>
      <td>
        {{ meta.now | date: "MMM Do, YYYY h:mm A" }}
      </td>
      <td>
        Jan 8th, 2019 8:56 AM
      </td>
    </tr>
    <tr>
      <td>
        {{ meta.now | date: "YYYY/MM/DD" }}
      </td>
      <td>
        2019/01/08
      </td>
    </tr>
  </tbody>
</table>

You can find the full list of formatting options in the Moment.js'
[documentation](https://momentjs.com/docs/#/displaying/format/).

## meta.preferences_url

The `meta.preferences_url` contains an URL to the preferences page specific
to each contact.

## meta.unsubscribe_url

The `meta.unsubscribe_url` contains an URL to a page which will unsubscribe
the contact from the targeted lists.

## meta.company

The `meta.company.name`, `meta.company.address`, and `meta.company.email`
variables contain information about the current project.

Continue to [Import](/templates/import.md).

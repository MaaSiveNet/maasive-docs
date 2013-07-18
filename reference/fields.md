#Fields

##Simple Fields

<table class="table table-bordered table-striped">
    <caption><em>Simple Field Types</em></caption>
    <thead><tr>
        <th>Field Name</th>
        <th>Field Description</th>
        <th>Field Aliases</th>
    </tr></thead>
    <tr>
        <td><code>String</code></td>
        <td>a standard unicode string of any length</td>
        <td>Unicode, StringField</td></tr>
    <tr>
        <td><code>Integer</code></td>
        <td>an integer</td>
        <td>IntegerField</td>
    </tr>
    <tr>
        <td><code>Object</code></td>
        <td>a JSON object that you can also think of as a dictionary or an associative array</td>
        <td>Dictionary</td>
    </tr>
    <tr>
        <td><code>List</code></td>
        <td>a JSON array that you can also think of as a list or integer indexed array</td>
        <td>Array, ListField</td>
    </tr>
    <tr>
        <td><code>Boolean</code></td>
        <td>true or false, it's as simple as that</td>
        <td>Bool, BooleanField</td>
    </tr>
    <tr>
        <td><code>Float</code></td>
        <td>a special field for floating point numbers</td>
        <td>FloatField</td>
    </tr>
</table>

##Complex Fields

<table class="table table-bordered table-striped">
    <caption><em>Complex Field Types</em></caption>
    <thead><tr>
        <th>Field Name</th>
        <th>Field Description</th>
        <th>Field Aliases</th>
    </tr></thead>
    <tr>
        <td><code>ObjectId</code></td>
        <td>a unique id for your resources with a built in timestamp</td>
        <td>ObjectIdField</td>
    </tr>
    <tr>
        <td><code>Email</code></td>
        <td>only properly constructed email addresses will validate in this field</td>
        <td>EmailField</td>
    </tr>
    <tr>
        <td><code>Address</code></td>
        <td>address is a compound field, itself an object with the keys: street1, street2, city, state,
        zip</td>
        <td>AddressField</td>
    </tr>
    <tr>
        <td><code>DateTime</code></td>
        <td>an iso time tuple</td>
        <td>DateTimeField</td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td></td>
    </tr>
</table>
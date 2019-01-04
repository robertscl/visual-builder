---
title: Input Designer
order: 2
layout: post
redirect_from: /docs/
---

## Zapier Input Designer

To build a Zapier integration, you need to do two things: tell Zapier how to connect to your API, and create forms where users can input data to send to your API.

Input Designer is built for the latter. Where every other step in building a Zapier integration asks you add to enter details in a form, here you _create_ a new form designed for the data your app needs.

Both Triggers and Actions can have an input form—but input forms are required in actions, as they always need a way for users to send data to your app to find, update, or create something new. Input Designer works the same in both.

## How to Use Zapier Input Designer

Input Designer works similarly to other form builder tools such as Wufoo or Google Forms, only here you’re building a form that lives inside your Zapier integration. Add fields to your form for each bit of data your app needs from users. Zapier uses `string` short text fields by default or you can choose from nine other field types to gather the data your app needs. Configure the field settings, then reorder them to match the logical order users would add data in your app.

### Add Fields

![Zapier Input Designer][image-1]

Zapier integrations can use three types of fields:

- **Input Fields** are the main type of field that most integrations use, with 10 field types to let users enter plain text data and map variables from previous triggers and actions into the field.
- **Dynamic Fields** make API calls to your app, then show the returned data in a dropdown menu so users can select the item needed, often used for folders, projects, assignees, and other data that would need to be chosen from your app.
- **Line Item Group** organize a set of Input Fields to create line items, where each item in a comma separated list entered in the field would create a new separate item in your app, often used for line items in invoice and accounting apps.

Most Zapier integrations rely on input fields. Integrations only need dynamic fields if users would need to select data from your app in the form, and would only need line items if users commonly add multiple lines of similar details to your app.

To add a field, click the _Add_ button and select the field type. Enter the field details, including:

- **Label**: A user friendly name for the field, such as `First Name`.
- **Key**: A unique identifier for the field, without spaces, ideally with the same key as your API, such as `first_name`.
- **Help Text**: (optional) A 20 character or longer description that appears under the field label, with [Markdown][1] formatting.
- **Type**: One of ten field types, with `String` as the default field type; see details on each field type below.
- **Default Text**: (optional) Copy to include in the field if the user doesn’t enter anything; only include if this copy would work in every user’s account.
- **Options**: (optional) Check whether this field should be required, if multiple values can be added, if the field is used to alter dynamic fields, or if it should be a dropdown.

Set each option and preview how your field looks inside a Zap on the right. When finished, click _Save_ then repeat the process to add each field your trigger or action step needs.

### Set Field Options



#### Required

![Zapier Required Field][image-2]

Have any fields your API _requires_ to included data in order to find or create something in your app? For example, if an email app like MailChimp requires an email address to add a new email subscription, and a calendar app like Google Calendar requires an event title, date, and time to add new events.

If your trigger or action step requires any data, check the _Required_ box on those fields. Zapier will show a red `(required)` label beside the field name, and will not let users complete the Zap step without adding data to that field.

Be sure to include a description on required fields to let users know exactly what type of data they should add to this field so the integration will work as expected. Also, never mark fields as required if the integration could work without them.

#### Allows Multiples

![Zapier Field Allows Multiples][image-3]

Have a field where users could add multiple entries in the same field? For example, Gmail’s integration lets users add multiple tags to email messages. For fields like this, check the _Allows Multiples_ box.

That adds a `+` button on the far right side of your field inside Zaps; users can click that to add another entry to the field. Zapier’s platform then delivers each entry in a comma separated list to your API.

#### Alters Dynamic Fields

If you have dynamic fields in your integration, where Zapier runs code to decide whether to show a field or what to show in a field, you can use other input fields to modify those dynamic fields.

Say you have a field that is only shown depending on the value of a previous field. The latter field should have the _Alters Dynamic Fields_ option checked, then the previous field should be a dynamic field with code to watch for the value of that field. Or, say your app lets users manage personal and work tasks, and add tasks to the correct project. You could first let them choose whether they’re adding personal or work tasks, and mark that field as _Alters Dynamic Fields_. Then you would add a Dynamic Field to your Input Form that uses this field and fetches the appropriate projects from your app.

If you check the _Alters Dynamic Fields_ option on a field, Zapier will automatically recompute any dynamic fields in your Zapier integration anytime this field is changed. Do not check the _Alters Dynamic Fields_ box unless the field is needed for your integrations’ dynamic fields.

<a id="dropdown"></a>
#### Dropdown

![Zapier form field dropdown][image-4]

Need to offer users pre-set options to choose from in a field? Make sure your field type is set as `String`, then check the _Dropdown_ box.

That opens two options: the default _Static_ as pictured above, or _Dynamic_. To add a Static menu of choices, type the options in a comma separated list, with quotes around each item and square brackets around the set, such as:

`["one", "two","three"]`

Enter the fields as used in your API, as Zapier will pass the exact value users select to your app. In the Zap editor, though, Zapier will capitalize each item in your dropdown menu, and will add spaces instead of any underscores, so an option like `first_name` would show in the menu as `First Name`.

![Zapier Add Dynamic Dropdown Field][image-5]

To add a dynamic dropdown field, you first need to build a trigger in your integration that can fetch the data needed in that menu from your API, such as project or folder names. Then, select the _Dynamic_ option after checking the _Dropdown_ box, and choose the trigger from which Zapier should fetch the data. Finally, enter the field name from your trigger, with the exact field ID of the trigger output field that you want Zapier to show, and add a user-friendly label to the field.

Whenever someone uses this input field in a Zap and selects this dynamic dropdown field, Zapier will poll your API for the data from that trigger, parse the entries from that field name, and show them in a user friendly dropdown menu.

Do note that users can always choose to enter a custom value as the final option in dropdown fields, to map data from other Zap steps into this field.

### Reorder Fields

![Reorder Input Fields Zapier][image-6]
_Change the order of input fields with the arrows, and preview the completed form on the right_

Add a field that should be at the top or bottom of your form? You can reorder input fields from the Form Editor screen. Click the up or down arrows to move the fields to the order you want. The preview on the right shows how the finished form looks to users inside Zapier.

It’s worth thinking through your form field order to make your integration as easy to use as possible. Put the most important, required fields first, with less important, optional fields near the bottom. Put related fields (such as first and last name) near each other. If your app includes a similar input form to create new items, you could order fields in Zapier similar to those in your app to increase ease of use.

### Remove Fields

![Delete Input Fields][image-7]
_Delete any fields that aren’t needed in your integration_

Add too many fields, and decide you don’t need one? Or want to start over with a new field?

Open the Input Designer, click the gear icon beside the field you want to delete, then select _Delete_. Zapier will ask you to confirm; click again to fully remove that field from your integration.

Note that you cannot restore a previous version of your input form, so be sure to only delete unnecessary fields, and never remove input fields from live integrations. Instead, make a new version of your integration before changing input fields.

## Zapier Input Field Types

Zapier includes ten different input field types to gather the specific data your app need for any Zap step. Each field shows the user which type of data to include—though do note that Zapier does not validate the data to ensure users added the correct item for that fieldtype. New input fields use the most versatile `String` option by default, but here are the details on each field type you can use to build integrations that work best with your app:

### String

![Zapier String Field][image-8]

The default Zapier input field, a String field shows a blank line for text. Typically used to gather individual text values such as a name, email address, or other details.

### Text

![Zapier Text Field][image-9]

Text fields are for longer text. Users can easily write a few lines of text, often used to enter email messages, notes, and other longer info.

### Integer

![Zapier Integer Field][image-10]

Integer fields are designed to gather integer number values, with a `1 2 3` tag beside the field in Zaps. They’re often used in Zapier along with a Dropdown field to select ID numbers for users, projects, and other internal data from apps, but can also be used to gather numbers.

### Number

![Zapier Number Field][image-11]

Number fields can gather numbers with any value, including decimal points, and show a `1.0` tag beside the field in Zaps. They’re most commonly used to gather numbers for integrations.

### Boolean

![Zapier Boolean Field][image-12]
  
Boolean fields let users select between `yes` and `no` values to set default settings in integrations, and return a corresponding `1` or `0` to your app. These are the simplest dropdown menus in Zaps.

### DateTime

![Zapier DateTime Field][image-13]

DateTime fields let users enter dates and times, using their human readable values, machine readable datetimes, or standard English words for time like `tomorrow`. Zapier interperpates the date input from users and outputs a standard UNIX time to your API.

> Learn more about how users can [modify dates and times in Zapier][2].

### File

![Zapier File Field][image-14]

File fields let users select a file object from a previous Zap step or enter a public URL to a file, where Zapier will then send the file to your API.

### Password

![Zapier Password Field][image-15]

Password fields work the same as standard string fields, except they hide the text entered in the field. They’re most commonly used in Authentication fields, especially for Basic Auth, but can be used in an integration if your app asks users to enter sensitive data.

### Dictionary

![Zapier Dictionary Field][image-16]

Dictionary fields let users enter their own value sets, with a plain text name followed by a String field to enter or map data from previous Zap steps. Users can click the `+` button on the right to add additional dictionary field entries as well.

### Copy

![Zapier Copy field][image-17]

The Copy field is the only field that does not let users enter data, and it is not passed along to your API. Instead, this field shows the _Help Text_ field’s Markdown formatted text as a rich text note inside the Zap step. It’s a handy way to share additional details about what to enter in the integration or link to external documentation if users would need more help.

> Learn how to [format text in Markdown][3].

## How to Add a Line Item Group

Line Items are a useful way to add as much data to an app as users need, especially in invoices, orders, and other accounting work. Some items may only need one line item, say for orders where a customer purchases one thing. Others need three, or 15, and Zapier’s line items make it easy to automate either way.

Normal input fields in Zapier add one item each time the Zap runs. Fields inside a Line Item Group, however, are added once per comma separated value added to the field. Users would map, say, an order field containing `item1,item2,item3` and a price field with `1.99,12.95,9.99`, and Zapier would add three line item rows with each item and its correct price.

> Learn more about line items from Zapier’s [Line Item Guide][4] and our [Line Item Help Docs][5].

![Add Zapier Line Item Group][image-18]

If your app’s action step needs line items, select _Line Item Group_ when adding a new field in the Input Designer. Add a name for the group of fields, something users would recognize as being a set of values where each one would be added individually. Also add a key for the group so Zapier can identify it internally.

![Zapier Line Item Input Fields][image-19]

Then add input fields for each item to include in your line item group. Click _Add Line Item_, then add the input field details as with other input fields. The only differences are that these fields will show inside the Line Item field block in Zapier, and you can’t set these fields as allowing multiples or altering dynamic fields.

![Edit or remove Zapier line item group fields][image-20]

Need to remove or reorder line item input fields? Open your Line Item Group field, and each input field has a gear icon beside it to edit or delete the field. You can’t move fields up or down, but you could delete fields then re-add them at the end of the list to get achieve the field order your integration needs.

## How to Add Dynamic Fields

![Add Zapier Dynamic Field][image-21]

Dynamic Fields let Zapier run code to decide whether to show a field, and can dynamically set what to show in the field as well. First, make sure you’ve included at least one input field that has _Alters Dynamic Fields_ checked. Then, from the _Input Designer_, add a new field and choose _Dynamic Field_.

There, you can write Node.js code that evaluates data from previous fields (referenced with `bundle.inputData.field_key` where `field_key` is replaced with the actual key of the field that Zapier is evaluating) and includes logic and details on another field to show depending on the value of the former.

> Learn more about how to add custom fields in code with [Zapier’s Field Schema][6]

[1]:	https://zapier.com/blog/beginner-ultimate-guide-markdown/
[2]:	https://zapier.com/help/modifying-dates-and-times/
[3]:	https://zapier.com/blog/beginner-ultimate-guide-markdown/
[4]:	https://zapier.com/blog/formatter-line-item-automation/
[5]:	https://zapier.com/help/line-items/
[6]:	https://zapier.github.io/zapier-platform-schema/build/schema.html#fieldschema

[image-1]:	https://cdn.zapier.com/storage/photos/31dfcf36c01b0ee0db946a6a46c3de8c.png
[image-2]:	https://cdn.zapier.com/storage/photos/aba4afb45bd9dbd5ec8c5e4a4137636d.png
[image-3]:	https://cdn.zapier.com/storage/photos/842d24708f402853e08ce6fbc06d650c.png
[image-4]:	https://cdn.zapier.com/storage/photos/0cf01c1dd6923b09cbb2cff97f0d6906.png
[image-5]:	https://cdn.zapier.com/storage/photos/f70686a8b053b541388da667e602f5b5.png
[image-6]:	https://cdn.zapier.com/storage/photos/2e73521bfc2f99ff43e12b444226421b.gif
[image-7]:	https://cdn.zapier.com/storage/photos/f065e57e78c2c57c65827a611a3a3fb1.gif
[image-8]:	https://cdn.zapier.com/storage/photos/14d9254a5e1195d6fc8bf03743e35aba.png
[image-9]:	https://cdn.zapier.com/storage/photos/4a2561c266257c72f20acbf35bdadbbb.png
[image-10]:	https://cdn.zapier.com/storage/photos/5f172119f8e4c28cef88cc0b01e78539.png
[image-11]:	https://cdn.zapier.com/storage/photos/fdcbd1c11d748a58a88598c635705ec2.png
[image-12]:	https://cdn.zapier.com/storage/photos/abc4b4149e7768680910607a708e6c2a.png
[image-13]:	https://cdn.zapier.com/storage/photos/cafd896bfcf92977464de936bdb4049b.png
[image-14]:	https://cdn.zapier.com/storage/photos/d6198c63b6adfd6d2d36ddcc49118acf.png
[image-15]:	https://cdn.zapier.com/storage/photos/ba63e87ff25ed2f16eb2bf538ad3ec48.png
[image-16]:	https://cdn.zapier.com/storage/photos/184904cd7048a06caed45b9575565096.png
[image-17]:	https://cdn.zapier.com/storage/photos/997589da843fbd06f89c18beb9e9ae02.png
[image-18]:	https://cdn.zapier.com/storage/photos/39e7e2296b66de0a9edea5ccef08c505.png
[image-19]:	https://cdn.zapier.com/storage/photos/5dcf22f358eb16c18abea7e532137269.png
[image-20]:	https://cdn.zapier.com/storage/photos/abf8f19ef35997b8919888da91b88590.png
[image-21]:	https://cdn.zapier.com/storage/photos/fdfe0ef4278760b1c22b47b6b66cb290.png
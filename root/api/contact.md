---
description: All wechat contacts(friend) will be encapsulated as a Contact.
---

# Contact

## Classes

[Contact](contact.md#Contact)

All wechat contacts\(friend\) will be encapsulated as a Contact. [Examples/Contact-Bot](https://github.com/Chatie/wechaty/blob/1523c5e02be46ebe2cc172a744b2fbe53351540e/examples/contact-bot.ts)

## Typedefs

[ContactQueryFilter](contact.md#ContactQueryFilter)

The way to search Contact

## Contact

All wechat contacts\(friend\) will be encapsulated as a Contact. [Examples/Contact-Bot](https://github.com/Chatie/wechaty/blob/1523c5e02be46ebe2cc172a744b2fbe53351540e/examples/contact-bot.ts)

**Kind**: global class  
**Properties**

| Name | Type | Description |
| :--- | :--- | :--- |
| id | `string` | Get Contact id. This function is depending on the Puppet Implementation, see [puppet-compatible-table](https://github.com/Chatie/wechaty/wiki/Puppet#3-puppet-compatible-table) |

* [Contact](contact.md#Contact)
  * _instance_
    * [.say\(textOrContactOrFileOrUrl\)](contact.md#Contact+say) ⇒ `Promise.`
    * [.name\(\)](contact.md#Contact+name) ⇒ `string`
    * [.alias\(newAlias\)](contact.md#Contact+alias) ⇒ `Promise.`
    * [.friend\(\)](contact.md#Contact+friend) ⇒ `boolean` \| `null`
    * [.type\(\)](contact.md#Contact+type) ⇒ `ContactType.Unknown` \| `ContactType.Personal` \| `ContactType.Official`
    * [.gender\(\)](contact.md#Contact+gender) ⇒ `ContactGender.Unknown` \| `ContactGender.Male` \| `ContactGender.Female`
    * [.province\(\)](contact.md#Contact+province) ⇒ `string` \| `null`
    * [.city\(\)](contact.md#Contact+city) ⇒ `string` \| `null`
    * [.avatar\(\)](contact.md#Contact+avatar) ⇒ `Promise.`
    * [.sync\(\)](contact.md#Contact+sync) ⇒ `Promise.`
    * [.self\(\)](contact.md#Contact+self) ⇒ `boolean`
  * _static_
    * [.find\(query\)](contact.md#Contact.find) ⇒ `Promise.`
    * [.findAll\(\[queryArg\]\)](contact.md#Contact.findAll) ⇒ `Promise.`

### contact.say\(textOrContactOrFileOrUrl\) ⇒ `Promise.`

> Tips: This function is depending on the Puppet Implementation, see [puppet-compatible-table](https://github.com/Chatie/wechaty/wiki/Puppet#3-puppet-compatible-table)

**Kind**: instance method of [`Contact`](contact.md#Contact)

| Param | Type | Description |
| :--- | :--- | :--- |
| textOrContactOrFileOrUrl | `string` \| [`Contact`](contact.md#Contact) \| `FileBox` \| `UrlLink` | send text, Contact, file or UrlLink to contact. &lt;/br&gt; You can use [FileBox](https://www.npmjs.com/package/file-box) to send file |

**Example**

```javascript
const bot = new Wechaty()
await bot.start()
const contact = await bot.Contact.find({name: 'lijiarui'})  // change 'lijiarui' to any of your contact name in wechat

// 1. send text to contact

await contact.say('welcome to wechaty!')

// 2. send media file to contact

import { FileBox }  from 'file-box'
const fileBox1 = FileBox.fromUrl('https://chatie.io/wechaty/images/bot-qr-code.png')
const fileBox2 = FileBox.fromFile('/tmp/text.txt')
await contact.say(fileBox1)
await contact.say(fileBox2)

// 3. send contact card to contact

const contactCard = bot.Contact.load('contactId')
await contact.say(contactCard)

// 4. send url link to contact
const linkPayload = new UrlLink({
  description : 'WeChat Bot SDK for Individual Account, Powered by TypeScript, Docker, and Love',
  thumbnailUrl: 'https://avatars0.githubusercontent.com/u/25162437?s=200&v=4',
  title       : 'Welcome to Wechaty',
  url         : 'https://github.com/chatie/wechaty',
})
await contact.say(urlLink)
```

### contact.name\(\) ⇒ `string`

Get the name from a contact

**Kind**: instance method of [`Contact`](contact.md#Contact)  
**Example**

```javascript
const name = contact.name()
```

### contact.alias\(newAlias\) ⇒ `Promise.`

GET / SET / DELETE the alias for a contact

Tests show it will failed if set alias too frequently\(60 times in one minute\).

**Kind**: instance method of [`Contact`](contact.md#Contact)

| Param | Type |
| :--- | :--- |
| newAlias | `none` \| `string` \| `null` |

**Example** _\( GET the alias for a contact, return {\(Promise&lt;string \| null&gt;\)}\)_

```javascript
const alias = await contact.alias()
if (alias === null) {
  console.log('You have not yet set any alias for contact ' + contact.name())
} else {
  console.log('You have already set an alias for contact ' + contact.name() + ':' + alias)
}
```

**Example** _\(SET the alias for a contact\)_

```javascript
try {
  await contact.alias('lijiarui')
  console.log(`change ${contact.name()}'s alias successfully!`)
} catch (e) {
  console.log(`failed to change ${contact.name()} alias!`)
}
```

**Example** _\(DELETE the alias for a contact\)_

```javascript
try {
  const oldAlias = await contact.alias(null)
  console.log(`delete ${contact.name()}'s alias successfully!`)
  console.log('old alias is ${oldAlias}`)
} catch (e) {
  console.log(`failed to delete ${contact.name()}'s alias!`)
}
```

### contact.friend\(\) ⇒ `boolean` \| `null`

Check if contact is friend

> Tips: This function is depending on the Puppet Implementation, see [puppet-compatible-table](https://github.com/Chatie/wechaty/wiki/Puppet#3-puppet-compatible-table)

**Kind**: instance method of [`Contact`](contact.md#Contact)  
**Returns**: `boolean` \| `null` -  
True for friend of the bot  
False for not friend of the bot, null for unknown.  
**Example**

```javascript
const isFriend = contact.friend()
```

### contact.type\(\) ⇒ `ContactType.Unknown` \| `ContactType.Personal` \| `ContactType.Official`

Return the type of the Contact

> Tips: ContactType is enum here.&lt;/br&gt;

**Kind**: instance method of [`Contact`](contact.md#Contact)  
**Example**

```javascript
const bot = new Wechaty()
await bot.start()
const isOfficial = contact.type() === bot.Contact.Type.Official
```

### contact.gender\(\) ⇒ `ContactGender.Unknown` \| `ContactGender.Male` \| `ContactGender.Female`

Contact gender

> Tips: ContactGender is enum here. &lt;/br&gt;

**Kind**: instance method of [`Contact`](contact.md#Contact)  
**Example**

```javascript
const gender = contact.gender() === bot.Contact.Gender.Male
```

### contact.province\(\) ⇒ `string` \| `null`

Get the region 'province' from a contact

**Kind**: instance method of [`Contact`](contact.md#Contact)  
**Example**

```javascript
const province = contact.province()
```

### contact.city\(\) ⇒ `string` \| `null`

Get the region 'city' from a contact

**Kind**: instance method of [`Contact`](contact.md#Contact)  
**Example**

```javascript
const city = contact.city()
```

### contact.avatar\(\) ⇒ `Promise.`

Get avatar picture file stream

**Kind**: instance method of [`Contact`](contact.md#Contact)  
**Example**

```javascript
// Save avatar to local file like `1-name.jpg`

const file = await contact.avatar()
const name = file.name
await file.toFile(name, true)
console.log(`Contact: ${contact.name()} with avatar file: ${name}`)
```

### contact.sync\(\) ⇒ `Promise.`

Force reload data for Contact, Sync data from lowlevel API again.

**Kind**: instance method of [`Contact`](contact.md#Contact)  
**Example**

```javascript
await contact.sync()
```

### contact.self\(\) ⇒ `boolean`

Check if contact is self

**Kind**: instance method of [`Contact`](contact.md#Contact)  
**Returns**: `boolean` - True for contact is self, False for contact is others  
**Example**

```javascript
const isSelf = contact.self()
```

### Contact.find\(query\) ⇒ `Promise.`

Try to find a contact by filter: {name: string \| RegExp} / {alias: string \| RegExp}

Find contact by name or alias, if the result more than one, return the first one.

**Kind**: static method of [`Contact`](contact.md#Contact)  
**Returns**: `Promise.` - If can find the contact, return Contact, or return null

| Param | Type |
| :--- | :--- |
| query | [`ContactQueryFilter`](contact.md#ContactQueryFilter) |

**Example**

```javascript
const bot = new Wechaty()
await bot.start()
const contactFindByName = await bot.Contact.find({ name:"ruirui"} )
const contactFindByAlias = await bot.Contact.find({ alias:"lijiarui"} )
```

### Contact.findAll\(\[queryArg\]\) ⇒ `Promise.`

Find contact by `name` or `alias`

If use Contact.findAll\(\) get the contact list of the bot.

#### definition

* `name`   the name-string set by user-self, should be called name
* `alias`  the name-string set by bot for others, should be called alias

**Kind**: static method of [`Contact`](contact.md#Contact)

| Param | Type |
| :--- | :--- |
| \[queryArg\] | [`ContactQueryFilter`](contact.md#ContactQueryFilter) |

**Example**

```javascript
const bot = new Wechaty()
await bot.start()
const contactList = await bot.Contact.findAll()                      // get the contact list of the bot
const contactList = await bot.Contact.findAll({ name: 'ruirui' })    // find allof the contacts whose name is 'ruirui'
const contactList = await bot.Contact.findAll({ alias: 'lijiarui' }) // find all of the contacts whose alias is 'lijiarui'
```

## ContactQueryFilter

The way to search Contact

**Kind**: global typedef  
**Properties**

| Name | Type | Description |
| :--- | :--- | :--- |
| name | `string` | The name-string set by user-self, should be called name |
| alias | `string` | The name-string set by bot for others, should be called alias [More Detail](https://github.com/Chatie/wechaty/issues/365) |


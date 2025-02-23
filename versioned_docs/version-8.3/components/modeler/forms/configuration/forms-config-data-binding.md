---
id: forms-config-data-binding
title: Data binding
description: How data from the process interacts with your form
---

## Binding form fields to process data

### Overview

Each **form element** that allows data manipulation is considered a **form field** and has a **Key** attribute. The "Key" serves a dual purpose:

1. To map data to the field during the initial loading of the form.
2. To map the field's data back to the process variable during form submission.

When a form is part of a user task or start event and viewed in [Tasklist](../../../tasklist/introduction-to-tasklist.md), the "Key" correlates with a process variable. This variable serves as the initial value of the field and is updated upon form submission.

### Simple key vs path key

#### Simple key

Traditionally, a key was defined as a simple variable name. This key directly matches a process variable.

```
key: "username"
```

#### Path as key

With newer updates, keys can now also be defined as a path, like `user.info.age`. This allows for more complex data structures.

```
key: "user.info.age"
```

Setting this field to value `21` would lead to the following output data:

```
{
  "user": {
	"info": {
      "age": 21
	}
  }
}
```

### Path extension via groups

In a form that utilizes **groups**, the group's **path** acts as a prefix to the key of each child field within that group. This effectively extends the key and allows for more intricate data mapping.

For example, if the group's path is `user.data`, and a child field has a key of `age`, the complete key would become `user.info.age`. This is particularly useful to deal with nested data structure inputs and outputs.

![Group Example Image](../assets/group-mapping-example.png)

If the above group has a path set to `user.data`, and if each field's key matches its label, the resulting output data will look like this:

```
{
  "user": {
    "data": {
      "surname": "Inco",
      "name": "Gnito",
      "age": 29
    }
  }
}
```

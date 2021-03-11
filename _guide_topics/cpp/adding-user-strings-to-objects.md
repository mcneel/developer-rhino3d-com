---
title: Adding User Strings to Objects
description: This guide discusses attaching custom user data to any object using the Rhino C/C++ SDK.
authors: ['dale_fugier']
sdk: ['C/C++']
languages: ['C/C++']
platforms: ['Windows']
categories: ['Fundamentals']
origin: http://wiki.mcneel.com/developer/sdksamples/setuserstring
order: 1
keywords: ['rhino', 'user', 'data']
layout: toc-guide-page
---

 
## Overview

User Data is a powerful set of APIs that allow plugin developers to attach custom data of any kind to any object derived from `ON_Object`.  In order to take advantage of User Data, you are required to implement your own user data object by deriving a class from `ON_UserData` and overriding the required virtual functions.

In Rhino, the SDK adds a new standardized approach for adding User Data to objects called User Strings.  The Rhino C/C++ SDK allows you to quickly attaches User Data in the form of a key-value string pair to any object derived from `ON_Object`.  This feature is exposed to the C/C++ SDK as member functions on `ON_Object`:

- `ON_Object::SetUserString`: attaches a user string to an object. This information will persist through copy construction, operator=, and file IO.
- `ON_Object::GetUserString`: gets a user string from an object.
- `ON_Object::GetUserStringKeys`: retrieves a list of all user string keys on an object.
- `ON_Object::GetUserStrings`: retrieves a list of all user strings on an object.

There are a number of advantages to User Strings:

- The mechanism is very simple - you do not have to derive any new classes.
- Rhino is responsible for all of the file IO.
- User Strings can hold text of any length and format, including XML. (length is currently limited to approximately 16MB)
- Since the mechanism is standard, user strings can shared between Rhino and other plugins.  For example, you can use Rhino's *GetUserText* and *SetUserText* commands to get and set user strings.

## Example

The following example demonstrates how to add User Strings to a selected object...

```cpp
CRhinoCommand::result CCommandTest::RunCommand( const CRhinoCommandContext& context )
{
  bool bAttribute = true;

  CRhinoGetObject go;
  go.SetCommandPrompt( L"Select object to attach user text" );
  go.AddCommandOptionToggle(
        RHCMDOPTNAME(L"Location"),
        RHCMDOPTVALUE(L"Object"),
        RHCMDOPTVALUE(L"Attribute"),
        bAttribute,
        &bAttribute
        );

  for(;;)
  {
    CRhinoGet::result res = go.GetObjects( 1, 1 );
    if( res == CRhinoGet::option )
      continue;
    if( res != CRhinoGet::object )
      return cancel;
    break;
  }

  const CRhinoObjRef& ref = go.Object(0);
  const CRhinoObject* obj = ref.Object();
  if( !obj )
    return failure;

  ON_wString key = L"test";
  ON_wString text = L"sample text";

  if( bAttribute )
  {
    // Attach user string to object's attributes
    CRhinoObjectAttributes attribs = obj->Attributes();
    attribs.SetUserString( key, text );
    context.m_doc.ModifyObjectAttributes( ref, attribs );
  }
  else
  {
    // Attach user string to object's geometry
    CRhinoObject* dupe = obj->DuplicateRhinoObject();
    if( dupe )
    {
      ON_Geometry* geom = const_cast<ON_Geometry*>( dupe->Geometry() );
      if( geom )
      {
        geom->SetUserString( key, text );
        context.m_doc.ReplaceObject( ref, dupe );
      }
    }
  }

  return success;
}
```

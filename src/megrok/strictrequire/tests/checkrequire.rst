"""
.. :doctest:

It is important to have all views closed by default, unless explicitely opened
up. Here we check to see that all view related component at have an explicitly
set `grok.require` directive.

This "assurance" is implemented by a custom grokker that checks whether a view
component does have a required permission defined::

    >>> from grokcore.component.testing import grok_component
    >>> from megrok.strictrequire.tests.fixtures import (
    ...     NoRequireView, NoRequirePage, NoRequireViewlet)
    >>> grok_component('NoRequireView', NoRequireView)
    Traceback (most recent call last):
    ...
    megrok.strictrequire.meta.SecurityError: megrok.strictrequire requires <class 'megrok.strictrequire.tests.fixtures.NoRequireView'> to use the grok.require directive!

    >>> grok_component('NoRequirePage', NoRequirePage)
    Traceback (most recent call last):
    ...
    megrok.strictrequire.meta.SecurityError: megrok.strictrequire requires <class 'megrok.strictrequire.tests.fixtures.NoRequirePage'> to use the grok.require directive!

    >>> grok_component('NoRequireViewlet', NoRequireViewlet)
    Traceback (most recent call last):
    ...
    megrok.strictrequire.meta.SecurityError: megrok.strictrequire requires <class 'megrok.strictrequire.tests.fixtures.NoRequireViewlet'> to use the grok.require directive!

Ditto for grok.Form, grok.AddForm. grok.EditForm, grok.XMLRPC, grok.JSON,
grok.REST components::

    >>> from megrok.strictrequire.tests.fixtures import (
    ...     NoRequireForm, NoRequireAddForm, NoRequireEditForm,
    ...     NoRequireXMLRPC, NoRequireREST, NoRequireJSON)
    >>> grok_component('NoRequireForm', NoRequireForm)
    Traceback (most recent call last):
    ...
    megrok.strictrequire.meta.SecurityError: megrok.strictrequire requires <class 'megrok.strictrequire.tests.fixtures.NoRequireForm'> to use the grok.require directive!

    >>> grok_component('NoRequireAddForm', NoRequireAddForm)
    Traceback (most recent call last):
    ...
    megrok.strictrequire.meta.SecurityError: megrok.strictrequire requires <class 'megrok.strictrequire.tests.fixtures.NoRequireAddForm'> to use the grok.require directive!

    >>> grok_component('NoRequireEditForm', NoRequireEditForm)
    Traceback (most recent call last):
    ...
    megrok.strictrequire.meta.SecurityError: megrok.strictrequire requires <class 'megrok.strictrequire.tests.fixtures.NoRequireEditForm'> to use the grok.require directive!

    >>> grok_component('NoRequireXMLRPC', NoRequireXMLRPC)
    Traceback (most recent call last):
    ...
    megrok.strictrequire.meta.SecurityError: megrok.strictrequire requires <class 'megrok.strictrequire.tests.fixtures.NoRequireXMLRPC'> to use the grok.require directive on the method:...NoRequireXMLRPC.foobar...

    >>> grok_component('NoRequireREST', NoRequireREST)
    Traceback (most recent call last):
    ...
    megrok.strictrequire.meta.SecurityError: megrok.strictrequire requires <class 'megrok.strictrequire.tests.fixtures.NoRequireREST'> to use the grok.require directive on the method:...NoRequireREST.foobar...

    >>> grok_component('NoRequireJSON', NoRequireJSON)
    Traceback (most recent call last):
    ...
    megrok.strictrequire.meta.SecurityError: megrok.strictrequire requires <class 'megrok.strictrequire.tests.fixtures.NoRequireJSON'> to use the grok.require directive on the method:...NoRequireJSON.foobar...

Of course, when the grok.require directive *is* used, there should not be any
exception raised::

    >>> from megrok.strictrequire.tests.fixtures import (
    ...     RequireView, RequirePage, RequireForm, RequireAddForm,
    ...     RequireEditForm, RequireXMLRPC, RequireREST, RequireJSON,
    ...     RequireOnMethodXMLRPC, RequireOnMethodREST, RequireOnMethodJSON)
    >>> grok_component('RequireView', RequireView)
    True
    >>> grok_component('RequirePage', RequirePage)
    True
    >>> grok_component('RequireForm', RequireForm)
    True
    >>> grok_component('RequireAddForm', RequireAddForm)
    True
    >>> grok_component('RequireEditForm', RequireEditForm)
    True
    >>> grok_component('RequireXMLRPC', RequireXMLRPC)
    True
    >>> grok_component('RequireREST', RequireREST)
    True
    >>> grok_component('RequireJSON', RequireJSON)
    True
    >>> grok_component('RequireOnMethodXMLRPC', RequireOnMethodXMLRPC)
    True
    >>> grok_component('RequireOnMethodREST', RequireOnMethodREST)
    True
    >>> grok_component('RequireOnMethodJSON', RequireOnMethodJSON)
    True

"""

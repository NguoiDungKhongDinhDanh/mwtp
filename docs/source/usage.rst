Usage
=====

The parser works as simple as follows:

.. code-block:: python

	from mwtp import TitleParser as Parser

	parser = Parser(namespaces_data, namespace_aliases)
	title = parser.parse(' _ FoO: this/is A\__/talk page _ ')

	print(repr(title))
	# Title('Talk:This/is A /talk page')

``namespaces_data`` and ``namespace_aliases`` can be obtained by
making a query to a wiki's API with
``action=query&meta=siteinfo&siprop=namespaces|namespacealiases``.
Here's how they might look like:

.. code-block:: python

	namespaces_data = {
	 '0': {
	   'id': 0,
	   'case': 'first-letter',
	   'name': '',
	   'subpages': False,
	   'content': True,
	   'nonincludable': False
	 },
	 '1': {
	   'id': 1,
	   'case': 'first-letter',
	   'name': 'Talk',
	   'subpages': True,
	   'canonical': 'Talk',
	   'content': False,
	   'nonincludable': False
	 },
	 ...: ...
	}
	namespace_aliases = [
	 { 'id': 1, 'alias': 'Foo' },
	 ...
	]

:meth:`~.TitleParser.parse` returns a :class:`.Title` object
which has a bunch of convenience properties for manipulating
titles:

.. code-block:: python

	title.namespace             # 1
	title.in_content_namespace  # False
	title.associated            # Title('This/is A /talk page')

A :class:`.Title` can be converted back to a :class:`str`
using either:

.. code-block:: python

	str(title)                  # 'Talk:This/is A /talk page'
	title.full_name             # 'Talk:This/is a /talk page'

See :class:`the class's full method list <.Title>` for more
information.
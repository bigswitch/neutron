Neutron Style Commandments
==========================

- Step 1: Read the OpenStack Style Commandments
  http://docs.openstack.org/developer/hacking/
- Step 2: Read on

Neutron Specific Commandments
-----------------------------

- [N319] Validate that debug level logs are not translated
- [N320] Validate that LOG messages, except debug ones, have translations
- [N321] Validate that jsonutils module is used instead of json
- [N322] Detect common errors with assert_called_once_with
- [N324] Prevent use of deprecated contextlib.nested.
- [N325] Python 3: Do not use xrange.
- [N326] Python 3: do not use basestring.
- [N327] Python 3: do not use dict.iteritems.
- [N328] Detect wrong usage with assertEqual
- [N329] Method's default argument shouldn't be mutable
- [N330] Use assertEqual(*empty*, observed) instead of
         assertEqual(observed, *empty*)
- [N331] Detect wrong usage with assertTrue(isinstance()).
- [N332] Use assertEqual(expected_http_code, observed_http_code) instead of
         assertEqual(observed_http_code, expected_http_code).
- [N333] Validate that LOG.warning is used instead of LOG.warn. The latter
  is deprecated.
- [N334] Use unittest2 uniformly across Neutron.
- [N340] Check usage of <module>.i18n (and neutron.i18n)
- [N341] Check usage of _ from python builtins

Creating Unit Tests
-------------------
For every new feature, unit tests should be created that both test and
(implicitly) document the usage of said feature. If submitting a patch for a
bug that had no unit test, a new passing unit test should be added. If a
submitted bug fix does have a unit test, be sure to add a new one that fails
without the patch and passes with the patch.

All unittest classes must ultimately inherit from testtools.TestCase. In the
Neutron test suite, this should be done by inheriting from
neutron.tests.base.BaseTestCase. If the third party unittest library has to
be used directly then it is recommended to use unittest2 as it contains bug
fixes to unittest for all versions of Python prior to version 3.5.

All setUp and tearDown methods must upcall using the super() method.
tearDown methods should be avoided and addCleanup calls should be preferred.
Never manually create tempfiles. Always use the tempfile fixtures from
the fixture library to ensure that they are cleaned up.

# boost_to_bamboo_junit.xsl
This is a simple xsl for migrating boost xml result to bamboo valid one

At least for me, it wasn't working directly. So I created a simple xsl script to make the transformation between boost testing xml and bamboo junit format. In order to work the boost test output should look like this

```
<TestResult>
<TestSuite name="Simple testcases" result="failed" assertions_passed="36" assertions_failed="10" expected_failures="0" test_cases_passed="3" test_cases_failed="2" test_cases_skipped="0" test_cases_aborted="0">
<TestCase name="test1" result="passed" assertions_passed="4" assertions_failed="0" expected_failures="0">
</TestCase>
<TestCase name="test2" result="passed" assertions_passed="1" assertions_failed="0" expected_failures="0">
</TestCase>
<TestCase name="test3" result="passed" assertions_passed="6" assertions_failed="0" expected_failures="0">
</TestCase>
<TestCase name="test4" result="failed" assertions_passed="11" assertions_failed="5" expected_failures="0" message="error 500">
</TestCase>
<TestCase name="test5" result="failed" assertions_passed="14" assertions_failed="5" expected_failures="0" message="error 404">
</TestCase>
</TestSuite>
</TestResult>
```

and after the xsl transformation the result becomes like this one

```
<?xml version="1.0"?>
<testsuites total="5" failures="2" skipped="0" not-run="0">
  <testsuite name="Simple testcases" result="Fail" executed="True" time="0" asserts="46">
    <testcase name="test1" result="Pass" executed="True" time="0" asserts="4"/>
    <testcase name="test2" result="Pass" executed="True" time="0" asserts="1"/>
    <testcase name="test3" result="Pass" executed="True" time="0" asserts="6"/>
    <testcase name="test4" result="Fail" executed="True" time="0" asserts="16">
      <failure type="failed test case" message="error 500"/>
    </testcase>
    <testcase name="test5" result="Fail" executed="True" time="0" asserts="19">
      <failure type="failed test case" message="error 404"/>
    </testcase>
  </testsuite>
</testsuites>
```
Hope it helps someone :)

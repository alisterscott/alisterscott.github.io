# Approval Testing

- Test behaviour not code
- If behaviour isn't simple, stable and well defined, don't use assertions
- Capture system behaviour, filter it and manage things in it
- Approval testing - reject it (a bug), intentional change, or ignore it (we don't care)
- [Blacklisting vs Whitelisting](https://dev.to/roesslerj/whitelist-testing-vs-blacklist-testing)
- More checks implies more effective but less maintainable
- Assertion based checking - start checking nothing but blacklist outcomes up front - repeat until bored - what are all failure modes
- Approval checking - start checking everything and whitelist outcomes on demand - repeat until maintenance feels manageable - is this change correct, incorrect, or uninteresting
- Legacy code - correct behaviour is what it does now - cannot change to get it under test, APIs may be lacking
- Characterization testing - what it does
- <a href="http://TextTest.org">TextTest.org</a> (open source)
- <a href="http://www.methodsandtools.com/archive/archive.php">http://www.methodsandtools.com/archive/archive.php</a>

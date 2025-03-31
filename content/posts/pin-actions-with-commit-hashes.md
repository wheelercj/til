+++
title = 'Pin GitHub Actions with commit hashes'
date = 2025-03-26T23:39:06-07:00
lastmod = 2025-03-30T19:26:54-07:00
+++

In GitHub Actions, it's great to be able to use actions written by others as part of an action you're writing. However, that comes with security risks. Even if you know a third-party action is safe now, it could become compromised in a way that compromises your entire repository even without you changing which version of the action you're using.

As an example, let's say your action includes these lines:

```yaml
- name: Do something
  uses: doSomethingCreator/doSomething@v2
```

The `@v2` pins the version of the third-party action to a Git tag. You might wonder, "how could that become compromised? The tag references part of the Git commit history! Even if malicious commits are added, the tag will stay where it is." The problem is that Git tags are not immutable. If someone adds malicious commits, they will probably also change which commit the tag references.

The solution is to pin the action to a full Git commit SHA like this:

```yaml
- name: Do something
  uses: doSomethingCreator/doSomething@c95fe1489396fe8a9eb87c0abf8aa5b2ef267fda
```

With that, even the action's owner cannot make you suddenly start running malicious code without getting a hash collision.

Pinning with commit hashes is especially important for third-party actions created by people you're not 100% sure you can trust.

## Further reading

- [Using third-party actions | GitHub Docs](https://docs.github.com/en/actions/security-for-github-actions/security-guides/security-hardening-for-github-actions?learn=getting_started#using-third-party-actions)
- [Immutable Actions ⦋GA⦌ · Issue \#592 · github/roadmap](https://github.com/github/roadmap/issues/592)

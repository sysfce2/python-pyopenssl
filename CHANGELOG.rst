Changelog
=========

Versions are year-based with a strict backward-compatibility policy.
The third digit is only for regressions.
UNRELEASED
----------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Deprecations:
^^^^^^^^^^^^^

Changes:
^^^^^^^^

- Added ``OpenSSL.SSL.Context.set_tls13_ciphersuites`` that allows the allowed TLS 1.3 ciphers.

25.1.0 (2025-05-17)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Deprecations:
^^^^^^^^^^^^^

- Attempting using any methods that mutate an ``OpenSSL.SSL.Context`` after it
  has been used to create an ``OpenSSL.SSL.Connection`` will emit a warning. In
  a future release, this will raise an exception.

Changes:
^^^^^^^^

* ``cryptography`` maximum version has been increased to 45.0.x.


25.0.0 (2025-01-12)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Deprecations:
^^^^^^^^^^^^^

Changes:
^^^^^^^^

- Corrected type annotations on ``Context.set_alpn_select_callback``, ``Context.set_session_cache_mode``, ``Context.set_options``, ``Context.set_mode``, ``X509.subject_name_hash``, and ``X509Store.load_locations``.
- Deprecated APIs are now marked using ``warnings.deprecated``. ``mypy`` will emit deprecation notices for them when used with ``--enable-error-code deprecated``.

24.3.0 (2024-11-27)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Removed the deprecated ``OpenSSL.crypto.CRL``, ``OpenSSL.crypto.Revoked``, ``OpenSSL.crypto.dump_crl``, and ``OpenSSL.crypto.load_crl``. ``cryptography.x509``'s CRL functionality should be used instead.
- Removed the deprecated ``OpenSSL.crypto.sign`` and ``OpenSSL.crypto.verify``. ``cryptography.hazmat.primitives.asymmetric``'s signature APIs should be used instead.

Deprecations:
^^^^^^^^^^^^^

- Deprecated ``OpenSSL.rand`` - callers should use ``os.urandom()`` instead.
- Deprecated ``add_extensions`` and ``get_extensions`` on ``OpenSSL.crypto.X509Req`` and ``OpenSSL.crypto.X509``. These should have been deprecated at the same time ``X509Extension`` was. Users should use pyca/cryptography's X.509 APIs instead.
- Deprecated ``OpenSSL.crypto.get_elliptic_curves`` and ``OpenSSL.crypto.get_elliptic_curve``, as well as passing the reult of them to ``OpenSSL.SSL.Context.set_tmp_ecdh``, users should instead pass curves from ``cryptography``.
- Deprecated passing ``X509`` objects to ``OpenSSL.SSL.Context.use_certificate``, ``OpenSSL.SSL.Connection.use_certificate``, ``OpenSSL.SSL.Context.add_extra_chain_cert``, and ``OpenSSL.SSL.Context.add_client_ca``, users should instead pass ``cryptography.x509.Certificate`` instances. This is in preparation for deprecating pyOpenSSL's ``X509`` entirely.
- Deprecated passing ``PKey`` objects to ``OpenSSL.SSL.Context.use_privatekey`` and ``OpenSSL.SSL.Connection.use_privatekey``, users should instead pass ``cryptography`` priate key instances. This is in preparation for deprecating pyOpenSSL's ``PKey`` entirely.

Changes:
^^^^^^^^

* ``cryptography`` maximum version has been increased to 44.0.x.
* ``OpenSSL.SSL.Connection.get_certificate``, ``OpenSSL.SSL.Connection.get_peer_certificate``, ``OpenSSL.SSL.Connection.get_peer_cert_chain``, and ``OpenSSL.SSL.Connection.get_verified_chain`` now take an ``as_cryptography`` keyword-argument. When ``True`` is passed then ``cryptography.x509.Certificate`` are returned, instead of ``OpenSSL.crypto.X509``. In the future, passing ``False`` (the default) will be deprecated.


24.2.1 (2024-07-20)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Deprecations:
^^^^^^^^^^^^^

Changes:
^^^^^^^^

- Fixed changelog to remove sphinx specific restructured text strings.


24.2.0 (2024-07-20)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Deprecations:
^^^^^^^^^^^^^

- Deprecated ``OpenSSL.crypto.X509Req``, ``OpenSSL.crypto.load_certificate_request``, ``OpenSSL.crypto.dump_certificate_request``. Instead, ``cryptography.x509.CertificateSigningRequest``, ``cryptography.x509.CertificateSigningRequestBuilder``, ``cryptography.x509.load_der_x509_csr``, or ``cryptography.x509.load_pem_x509_csr`` should be used.

Changes:
^^^^^^^^

- Added type hints for the ``SSL`` module.
  `#1308 <https://github.com/pyca/pyopenssl/pull/1308>`_.
- Changed ``OpenSSL.crypto.PKey.from_cryptography_key`` to accept public and private EC, ED25519, ED448 keys.
  `#1310 <https://github.com/pyca/pyopenssl/pull/1310>`_.

24.1.0 (2024-03-09)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Removed the deprecated ``OpenSSL.crypto.PKCS12`` and
  ``OpenSSL.crypto.NetscapeSPKI``. ``OpenSSL.crypto.PKCS12`` may be replaced
  by the PKCS#12 APIs in the ``cryptography`` package.

Deprecations:
^^^^^^^^^^^^^

Changes:
^^^^^^^^

24.0.0 (2024-01-22)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Deprecations:
^^^^^^^^^^^^^

Changes:
^^^^^^^^

- Added ``OpenSSL.SSL.Connection.get_selected_srtp_profile`` to determine which SRTP profile was negotiated.
  `#1279 <https://github.com/pyca/pyopenssl/pull/1279>`_.

23.3.0 (2023-10-25)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Dropped support for Python 3.6.
- The minimum ``cryptography`` version is now 41.0.5.
- Removed ``OpenSSL.crypto.load_pkcs7`` and ``OpenSSL.crypto.load_pkcs12`` which had been deprecated for 3 years.
- Added ``OpenSSL.SSL.OP_LEGACY_SERVER_CONNECT`` to allow legacy insecure renegotiation between OpenSSL and unpatched servers.
  `#1234 <https://github.com/pyca/pyopenssl/pull/1234>`_.

Deprecations:
^^^^^^^^^^^^^

- Deprecated ``OpenSSL.crypto.PKCS12`` (which was intended to have been deprecated at the same time as ``OpenSSL.crypto.load_pkcs12``).
- Deprecated ``OpenSSL.crypto.NetscapeSPKI``.
- Deprecated ``OpenSSL.crypto.CRL``
- Deprecated ``OpenSSL.crypto.Revoked``
- Deprecated ``OpenSSL.crypto.load_crl`` and ``OpenSSL.crypto.dump_crl``
- Deprecated ``OpenSSL.crypto.sign`` and ``OpenSSL.crypto.verify``
- Deprecated ``OpenSSL.crypto.X509Extension``

Changes:
^^^^^^^^

- Changed ``OpenSSL.crypto.X509Store.add_crl`` to also accept
  ``cryptography``'s ``x509.CertificateRevocationList`` arguments in addition
  to the now deprecated ``OpenSSL.crypto.CRL`` arguments.
- Fixed ``test_set_default_verify_paths`` test so that it is skipped if no
  network connection is available.

23.2.0 (2023-05-30)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Removed ``X509StoreFlags.NOTIFY_POLICY``.
  `#1213 <https://github.com/pyca/pyopenssl/pull/1213>`_.

Deprecations:
^^^^^^^^^^^^^

Changes:
^^^^^^^^

- ``cryptography`` maximum version has been increased to 41.0.x.
- Invalid versions are now rejected in ``OpenSSL.crypto.X509Req.set_version``.
- Added ``X509VerificationCodes`` to ``OpenSSL.SSL``.
  `#1202 <https://github.com/pyca/pyopenssl/pull/1202>`_.

23.1.1 (2023-03-28)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Deprecations:
^^^^^^^^^^^^^

Changes:
^^^^^^^^

- Worked around an issue in OpenSSL 3.1.0 which caused `X509Extension.get_short_name` to raise an exception when no short name was known to OpenSSL.
  `#1204 <https://github.com/pyca/pyopenssl/pull/1204>`_.

23.1.0 (2023-03-24)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Deprecations:
^^^^^^^^^^^^^

Changes:
^^^^^^^^

- ``cryptography`` maximum version has been increased to 40.0.x.
- Add ``OpenSSL.SSL.Connection.DTLSv1_get_timeout`` and ``OpenSSL.SSL.Connection.DTLSv1_handle_timeout``
  to support DTLS timeouts `#1180 <https://github.com/pyca/pyopenssl/pull/1180>`_.

23.0.0 (2023-01-01)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Deprecations:
^^^^^^^^^^^^^

Changes:
^^^^^^^^

- Add ``OpenSSL.SSL.X509StoreFlags.PARTIAL_CHAIN`` constant to allow for users
  to perform certificate verification on partial certificate chains.
  `#1166 <https://github.com/pyca/pyopenssl/pull/1166>`_
- ``cryptography`` maximum version has been increased to 39.0.x.

22.1.0 (2022-09-25)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Remove support for SSLv2 and SSLv3.
- The minimum ``cryptography`` version is now 38.0.x (and we now pin releases
  against ``cryptography`` major versions to prevent future breakage)
- The ``OpenSSL.crypto.X509StoreContextError`` exception has been refactored,
  changing its internal attributes.
  `#1133 <https://github.com/pyca/pyopenssl/pull/1133>`_

Deprecations:
^^^^^^^^^^^^^

- ``OpenSSL.SSL.SSLeay_version`` is deprecated in favor of
  ``OpenSSL.SSL.OpenSSL_version``. The constants ``OpenSSL.SSL.SSLEAY_*`` are
  deprecated in favor of ``OpenSSL.SSL.OPENSSL_*``.

Changes:
^^^^^^^^

- Add ``OpenSSL.SSL.Connection.set_verify`` and ``OpenSSL.SSL.Connection.get_verify_mode``
  to override the context object's verification flags.
  `#1073 <https://github.com/pyca/pyopenssl/pull/1073>`_
- Add ``OpenSSL.SSL.Connection.use_certificate`` and ``OpenSSL.SSL.Connection.use_privatekey``
  to set a certificate per connection (and not just per context) `#1121 <https://github.com/pyca/pyopenssl/pull/1121>`_.

22.0.0 (2022-01-29)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Drop support for Python 2.7.
  `#1047 <https://github.com/pyca/pyopenssl/pull/1047>`_
- The minimum ``cryptography`` version is now 35.0.

Deprecations:
^^^^^^^^^^^^^

Changes:
^^^^^^^^

- Expose wrappers for some `DTLS
  <https://en.wikipedia.org/wiki/Datagram_Transport_Layer_Security>`_
  primitives. `#1026 <https://github.com/pyca/pyopenssl/pull/1026>`_

21.0.0 (2021-09-28)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- The minimum ``cryptography`` version is now 3.3.
- Drop support for Python 3.5

Deprecations:
^^^^^^^^^^^^^

Changes:
^^^^^^^^

- Raise an error when an invalid ALPN value is set.
  `#993 <https://github.com/pyca/pyopenssl/pull/993>`_
- Added ``OpenSSL.SSL.Context.set_min_proto_version`` and ``OpenSSL.SSL.Context.set_max_proto_version``
  to set the minimum and maximum supported TLS version `#985 <https://github.com/pyca/pyopenssl/pull/985>`_.
- Updated ``to_cryptography`` and ``from_cryptography`` methods to support an upcoming release of ``cryptography`` without raising deprecation warnings.
  `#1030 <https://github.com/pyca/pyopenssl/pull/1030>`_

20.0.1 (2020-12-15)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Deprecations:
^^^^^^^^^^^^^

Changes:
^^^^^^^^

- Fixed compatibility with OpenSSL 1.1.0.

20.0.0 (2020-11-27)
-------------------


Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- The minimum ``cryptography`` version is now 3.2.
- Remove deprecated ``OpenSSL.tsafe`` module.
- Removed deprecated ``OpenSSL.SSL.Context.set_npn_advertise_callback``, ``OpenSSL.SSL.Context.set_npn_select_callback``, and ``OpenSSL.SSL.Connection.get_next_proto_negotiated``.
- Drop support for Python 3.4
- Drop support for OpenSSL 1.0.1 and 1.0.2

Deprecations:
^^^^^^^^^^^^^

- Deprecated ``OpenSSL.crypto.load_pkcs7`` and ``OpenSSL.crypto.load_pkcs12``.

Changes:
^^^^^^^^

- Added a new optional ``chain`` parameter to ``OpenSSL.crypto.X509StoreContext()``
  where additional untrusted certificates can be specified to help chain building.
  `#948 <https://github.com/pyca/pyopenssl/pull/948>`_
- Added ``OpenSSL.crypto.X509Store.load_locations`` to set trusted
  certificate file bundles and/or directories for verification.
  `#943 <https://github.com/pyca/pyopenssl/pull/943>`_
- Added ``Context.set_keylog_callback`` to log key material.
  `#910 <https://github.com/pyca/pyopenssl/pull/910>`_
- Added ``OpenSSL.SSL.Connection.get_verified_chain`` to retrieve the
  verified certificate chain of the peer.
  `#894 <https://github.com/pyca/pyopenssl/pull/894>`_.
- Make verification callback optional in ``Context.set_verify``.
  If omitted, OpenSSL's default verification is used.
  `#933 <https://github.com/pyca/pyopenssl/pull/933>`_
- Fixed a bug that could truncate or cause a zero-length key error due to a
  null byte in private key passphrase in ``OpenSSL.crypto.load_privatekey``
  and ``OpenSSL.crypto.dump_privatekey``.
  `#947 <https://github.com/pyca/pyopenssl/pull/947>`_

19.1.0 (2019-11-18)
-------------------


Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Removed deprecated ``ContextType``, ``ConnectionType``, ``PKeyType``, ``X509NameType``, ``X509ReqType``, ``X509Type``, ``X509StoreType``, ``CRLType``, ``PKCS7Type``, ``PKCS12Type``, and ``NetscapeSPKIType`` aliases.
  Use the classes without the ``Type`` suffix instead.
  `#814 <https://github.com/pyca/pyopenssl/pull/814>`_
- The minimum ``cryptography`` version is now 2.8 due to issues on macOS with a transitive dependency.
  `#875 <https://github.com/pyca/pyopenssl/pull/875>`_

Deprecations:
^^^^^^^^^^^^^

- Deprecated ``OpenSSL.SSL.Context.set_npn_advertise_callback``, ``OpenSSL.SSL.Context.set_npn_select_callback``, and ``OpenSSL.SSL.Connection.get_next_proto_negotiated``.
  ALPN should be used instead.
  `#820 <https://github.com/pyca/pyopenssl/pull/820>`_


Changes:
^^^^^^^^

- Support ``bytearray`` in ``SSL.Connection.send()`` by using cffi's from_buffer.
  `#852 <https://github.com/pyca/pyopenssl/pull/852>`_
- The ``OpenSSL.SSL.Context.set_alpn_select_callback`` can return a new ``NO_OVERLAPPING_PROTOCOLS`` sentinel value
  to allow a TLS handshake to complete without an application protocol.


----

19.0.0 (2019-01-21)
-------------------


Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- ``X509Store.add_cert`` no longer raises an error if you add a duplicate cert.
  `#787 <https://github.com/pyca/pyopenssl/pull/787>`_


Deprecations:
^^^^^^^^^^^^^

*none*


Changes:
^^^^^^^^

- pyOpenSSL now works with OpenSSL 1.1.1.
  `#805 <https://github.com/pyca/pyopenssl/pull/805>`_
- pyOpenSSL now handles NUL bytes in ``X509Name.get_components()``
  `#804 <https://github.com/pyca/pyopenssl/pull/804>`_



----

18.0.0 (2018-05-16)
-------------------


Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- The minimum ``cryptography`` version is now 2.2.1.
- Support for Python 2.6 has been dropped.


Deprecations:
^^^^^^^^^^^^^

*none*


Changes:
^^^^^^^^

- Added ``Connection.get_certificate`` to retrieve the local certificate.
  `#733 <https://github.com/pyca/pyopenssl/pull/733>`_
- ``OpenSSL.SSL.Connection`` now sets ``SSL_MODE_AUTO_RETRY`` by default.
  `#753 <https://github.com/pyca/pyopenssl/pull/753>`_
- Added ``Context.set_tlsext_use_srtp`` to enable negotiation of SRTP keying material.
  `#734 <https://github.com/pyca/pyopenssl/pull/734>`_


----

17.5.0 (2017-11-30)
-------------------


Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- The minimum ``cryptography`` version is now 2.1.4.


Deprecations:
^^^^^^^^^^^^^

*none*


Changes:
^^^^^^^^

- Fixed a potential use-after-free in the verify callback and resolved a memory leak when loading PKCS12 files with ``cacerts``.
  `#723 <https://github.com/pyca/pyopenssl/pull/723>`_
- Added ``Connection.export_keying_material`` for RFC 5705 compatible export of keying material.
  `#725 <https://github.com/pyca/pyopenssl/pull/725>`_

----



17.4.0 (2017-11-21)
-------------------


Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*none*


Deprecations:
^^^^^^^^^^^^^

*none*


Changes:
^^^^^^^^


- Re-added a subset of the ``OpenSSL.rand`` module.
  This subset allows conscientious users to reseed the OpenSSL CSPRNG after fork.
  `#708 <https://github.com/pyca/pyopenssl/pull/708>`_
- Corrected a use-after-free when reusing an issuer or subject from an ``X509`` object after the underlying object has been mutated.
  `#709 <https://github.com/pyca/pyopenssl/pull/709>`_

----


17.3.0 (2017-09-14)
-------------------


Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Dropped support for Python 3.3.
  `#677 <https://github.com/pyca/pyopenssl/pull/677>`_
- Removed the deprecated ``OpenSSL.rand`` module.
  This is being done ahead of our normal deprecation schedule due to its lack of use and the fact that it was becoming a maintenance burden.
  ``os.urandom()`` should be used instead.
  `#675 <https://github.com/pyca/pyopenssl/pull/675>`_


Deprecations:
^^^^^^^^^^^^^

- Deprecated ``OpenSSL.tsafe``.
  `#673 <https://github.com/pyca/pyopenssl/pull/673>`_

Changes:
^^^^^^^^

- Fixed a memory leak in ``OpenSSL.crypto.CRL``.
  `#690 <https://github.com/pyca/pyopenssl/pull/690>`_
- Fixed a memory leak when verifying certificates with ``OpenSSL.crypto.X509StoreContext``.
  `#691 <https://github.com/pyca/pyopenssl/pull/691>`_


----


17.2.0 (2017-07-20)
-------------------


Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*none*


Deprecations:
^^^^^^^^^^^^^

- Deprecated ``OpenSSL.rand`` - callers should use ``os.urandom()`` instead.
  `#658 <https://github.com/pyca/pyopenssl/pull/658>`_


Changes:
^^^^^^^^

- Fixed a bug causing ``Context.set_default_verify_paths()`` to not work with cryptography ``manylinux1`` wheels on Python 3.x.
  `#665 <https://github.com/pyca/pyopenssl/pull/665>`_
- Fixed a crash with (EC)DSA signatures in some cases.
  `#670 <https://github.com/pyca/pyopenssl/pull/670>`_


----


17.1.0 (2017-06-30)
-------------------


Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Removed the deprecated ``OpenSSL.rand.egd()`` function.
  Applications should prefer ``os.urandom()`` for random number generation.
  `#630 <https://github.com/pyca/pyopenssl/pull/630>`_
- Removed the deprecated default ``digest`` argument to ``OpenSSL.crypto.CRL.export()``.
  Callers must now always pass an explicit ``digest``.
  `#652 <https://github.com/pyca/pyopenssl/pull/652>`_
- Fixed a bug with ``ASN1_TIME`` casting in ``X509.set_notBefore()``,
  ``X509.set_notAfter()``, ``Revoked.set_rev_date()``, ``Revoked.set_nextUpdate()``,
  and ``Revoked.set_lastUpdate()``. You must now pass times in the form
  ``YYYYMMDDhhmmssZ``. ``YYYYMMDDhhmmss+hhmm`` and ``YYYYMMDDhhmmss-hhmm``
  will no longer work. `#612 <https://github.com/pyca/pyopenssl/pull/612>`_


Deprecations:
^^^^^^^^^^^^^


- Deprecated the legacy "Type" aliases: ``ContextType``, ``ConnectionType``, ``PKeyType``, ``X509NameType``, ``X509ExtensionType``, ``X509ReqType``, ``X509Type``, ``X509StoreType``, ``CRLType``, ``PKCS7Type``, ``PKCS12Type``, ``NetscapeSPKIType``.
  The names without the "Type"-suffix should be used instead.


Changes:
^^^^^^^^

- Added ``OpenSSL.crypto.X509.from_cryptography()`` and ``OpenSSL.crypto.X509.to_cryptography()`` for converting X.509 certificate to and from pyca/cryptography objects.
  `#640 <https://github.com/pyca/pyopenssl/pull/640>`_
- Added ``OpenSSL.crypto.X509Req.from_cryptography()``, ``OpenSSL.crypto.X509Req.to_cryptography()``, ``OpenSSL.crypto.CRL.from_cryptography()``, and ``OpenSSL.crypto.CRL.to_cryptography()`` for converting X.509 CSRs and CRLs to and from pyca/cryptography objects.
  `#645 <https://github.com/pyca/pyopenssl/pull/645>`_
- Added ``OpenSSL.debug`` that allows to get an overview of used library versions (including linked OpenSSL) and other useful runtime information using ``python -m OpenSSL.debug``.
  `#620 <https://github.com/pyca/pyopenssl/pull/620>`_
- Added a fallback path to ``Context.set_default_verify_paths()`` to accommodate the upcoming release of ``cryptography`` ``manylinux1`` wheels.
  `#633 <https://github.com/pyca/pyopenssl/pull/633>`_


----


17.0.0 (2017-04-20)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*none*


Deprecations:
^^^^^^^^^^^^^

*none*


Changes:
^^^^^^^^

- Added ``OpenSSL.X509Store.set_time()`` to set a custom verification time when verifying certificate chains.
  `#567 <https://github.com/pyca/pyopenssl/pull/567>`_
- Added a collection of functions for working with OCSP stapling.
  None of these functions make it possible to validate OCSP assertions, only to staple them into the handshake and to retrieve the stapled assertion if provided.
  Users will need to write their own code to handle OCSP assertions.
  We specifically added: ``Context.set_ocsp_server_callback()``, ``Context.set_ocsp_client_callback()``, and ``Connection.request_ocsp()``.
  `#580 <https://github.com/pyca/pyopenssl/pull/580>`_
- Changed the ``SSL`` module's memory allocation policy to avoid zeroing memory it allocates when unnecessary.
  This reduces CPU usage and memory allocation time by an amount proportional to the size of the allocation.
  For applications that process a lot of TLS data or that use very lage allocations this can provide considerable performance improvements.
  `#578 <https://github.com/pyca/pyopenssl/pull/578>`_
- Automatically set ``SSL_CTX_set_ecdh_auto()`` on ``OpenSSL.SSL.Context``.
  `#575 <https://github.com/pyca/pyopenssl/pull/575>`_
- Fix empty exceptions from ``OpenSSL.crypto.load_privatekey()``.
  `#581 <https://github.com/pyca/pyopenssl/pull/581>`_


----


16.2.0 (2016-10-15)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*none*


Deprecations:
^^^^^^^^^^^^^

*none*


Changes:
^^^^^^^^

- Fixed compatibility errors with OpenSSL 1.1.0.
- Fixed an issue that caused failures with subinterpreters and embedded Pythons.
  `#552 <https://github.com/pyca/pyopenssl/pull/552>`_


----


16.1.0 (2016-08-26)
-------------------

Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*none*


Deprecations:
^^^^^^^^^^^^^

- Dropped support for OpenSSL 0.9.8.


Changes:
^^^^^^^^

- Fix memory leak in ``OpenSSL.crypto.dump_privatekey()`` with ``FILETYPE_TEXT``.
  `#496 <https://github.com/pyca/pyopenssl/pull/496>`_
- Enable use of CRL (and more) in verify context.
  `#483 <https://github.com/pyca/pyopenssl/pull/483>`_
- ``OpenSSL.crypto.PKey`` can now be constructed from ``cryptography`` objects and also exported as such.
  `#439 <https://github.com/pyca/pyopenssl/pull/439>`_
- Support newer versions of ``cryptography`` which use opaque structs for OpenSSL 1.1.0 compatibility.


----


16.0.0 (2016-03-19)
-------------------

This is the first release under full stewardship of PyCA.
We have made *many* changes to make local development more pleasing.
The test suite now passes both on Linux and OS X with OpenSSL 0.9.8, 1.0.1, and 1.0.2.
It has been moved to `pytest <https://docs.pytest.org/>`_, all CI test runs are part of `tox <https://tox.readthedocs.io/>`_ and the source code has been made fully `flake8 <https://flake8.readthedocs.io/>`_ compliant.

We hope to have lowered the barrier for contributions significantly but are open to hear about any remaining frustrations.


Backward-incompatible changes:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Python 3.2 support has been dropped.
  It never had significant real world usage and has been dropped by our main dependency ``cryptography``.
  Affected users should upgrade to Python 3.3 or later.


Deprecations:
^^^^^^^^^^^^^

- The support for EGD has been removed.
  The only affected function ``OpenSSL.rand.egd()`` now uses ``os.urandom()`` to seed the internal PRNG instead.
  Please see `pyca/cryptography#1636 <https://github.com/pyca/cryptography/pull/1636>`_ for more background information on this decision.
  In accordance with our backward compatibility policy ``OpenSSL.rand.egd()`` will be *removed* no sooner than a year from the release of 16.0.0.

  Please note that you should `use urandom <https://sockpuppet.org/blog/2014/02/25/safely-generate-random-numbers/>`_ for all your secure random number needs.
- Python 2.6 support has been deprecated.
  Our main dependency ``cryptography`` deprecated 2.6 in version 0.9 (2015-05-14) with no time table for actually dropping it.
  pyOpenSSL will drop Python 2.6 support once ``cryptography`` does.


Changes:
^^^^^^^^

- Fixed ``OpenSSL.SSL.Context.set_session_id``, ``OpenSSL.SSL.Connection.renegotiate``, ``OpenSSL.SSL.Connection.renegotiate_pending``, and ``OpenSSL.SSL.Context.load_client_ca``.
  They were lacking an implementation since 0.14.
  `#422 <https://github.com/pyca/pyopenssl/pull/422>`_
- Fixed segmentation fault when using keys larger than 4096-bit to sign data.
  `#428 <https://github.com/pyca/pyopenssl/pull/428>`_
- Fixed ``AttributeError`` when ``OpenSSL.SSL.Connection.get_app_data()`` was called before setting any app data.
  `#304 <https://github.com/pyca/pyopenssl/pull/304>`_
- Added ``OpenSSL.crypto.dump_publickey()`` to dump ``OpenSSL.crypto.PKey`` objects that represent public keys, and ``OpenSSL.crypto.load_publickey()`` to load such objects from serialized representations.
  `#382 <https://github.com/pyca/pyopenssl/pull/382>`_
- Added ``OpenSSL.crypto.dump_crl()`` to dump a certificate revocation list out to a string buffer.
  `#368 <https://github.com/pyca/pyopenssl/pull/368>`_
- Added ``OpenSSL.SSL.Connection.get_state_string()`` using the OpenSSL binding ``state_string_long``.
  `#358 <https://github.com/pyca/pyopenssl/pull/358>`_
- Added support for the ``socket.MSG_PEEK`` flag to ``OpenSSL.SSL.Connection.recv()`` and ``OpenSSL.SSL.Connection.recv_into()``.
  `#294 <https://github.com/pyca/pyopenssl/pull/294>`_
- Added ``OpenSSL.SSL.Connection.get_protocol_version()`` and ``OpenSSL.SSL.Connection.get_protocol_version_name()``.
  `#244 <https://github.com/pyca/pyopenssl/pull/244>`_
- Switched to ``utf8string`` mask by default.
  OpenSSL formerly defaulted to a ``T61String`` if there were UTF-8 characters present.
  This was changed to default to ``UTF8String`` in the config around 2005, but the actual code didn't change it until late last year.
  This will default us to the setting that actually works.
  To revert this you can call ``OpenSSL.crypto._lib.ASN1_STRING_set_default_mask_asc(b"default")``.
  `#234 <https://github.com/pyca/pyopenssl/pull/234>`_


----


Older Changelog Entries
-----------------------

The changes from before release 16.0.0 are preserved in the `repository <https://github.com/pyca/pyopenssl/blob/master/doc/ChangeLog_old.txt>`_.

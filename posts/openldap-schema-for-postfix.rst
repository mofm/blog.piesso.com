.. title: OpenLDAP Schema for Postfix
.. slug: openldap-schema-for-postfix
.. date: 2018-03-31 20:43:33 UTC+03:00
.. tags: openldap, schema, postfix
.. category: 
.. link: 
.. description: 
.. type: text

If you configure postfix-dovecot with OpenLDAP, you will need specific LDAP's attributes. So I have written a schema.

postfix-new.schema:
	* 4 Attributes ( mailacceptinggeneralid, maildrop, mailEnabled, mailQuota )
	* 1 ObjectClass ( postfixUser )

.. gist:: 4eff37b5c0275416393344b687171848

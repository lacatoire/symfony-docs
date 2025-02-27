Ip
==

Validates that a value is a valid IP address. By default, this will validate
the value as IPv4, but a number of different options exist to validate as
IPv6 and many other combinations.

==========  ===================================================================
Applies to  :ref:`property or method <validation-property-target>`
Class       :class:`Symfony\\Component\\Validator\\Constraints\\Ip`
Validator   :class:`Symfony\\Component\\Validator\\Constraints\\IpValidator`
==========  ===================================================================

Basic Usage
-----------

.. configuration-block::

    .. code-block:: php-attributes

        // src/Entity/Author.php
        namespace App\Entity;

        use Symfony\Component\Validator\Constraints as Assert;

        class Author
        {
            #[Assert\Ip]
            protected string $ipAddress;
        }

    .. code-block:: yaml

        # config/validator/validation.yaml
        App\Entity\Author:
            properties:
                ipAddress:
                    - Ip: ~

    .. code-block:: xml

        <!-- config/validator/validation.xml -->
        <?xml version="1.0" encoding="UTF-8" ?>
        <constraint-mapping xmlns="http://symfony.com/schema/dic/constraint-mapping"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://symfony.com/schema/dic/constraint-mapping https://symfony.com/schema/dic/constraint-mapping/constraint-mapping-1.0.xsd">

            <class name="App\Entity\Author">
                <property name="ipAddress">
                    <constraint name="Ip"/>
                </property>
            </class>
        </constraint-mapping>

    .. code-block:: php

        // src/Entity/Author.php
        namespace App\Entity;

        use Symfony\Component\Validator\Constraints as Assert;
        use Symfony\Component\Validator\Mapping\ClassMetadata;

        class Author
        {
            // ...

            public static function loadValidatorMetadata(ClassMetadata $metadata): void
            {
                $metadata->addPropertyConstraint('ipAddress', new Assert\Ip());
            }
        }

.. include:: /reference/constraints/_empty-values-are-valid.rst.inc

Options
-------

.. include:: /reference/constraints/_groups-option.rst.inc

``message``
~~~~~~~~~~~

**type**: ``string`` **default**: ``This is not a valid IP address.``

This message is shown if the string is not a valid IP address.

You can use the following parameters in this message:

===============  ==============================================================
Parameter        Description
===============  ==============================================================
``{{ value }}``  The current (invalid) value
``{{ label }}``  Corresponding form field label
===============  ==============================================================

.. include:: /reference/constraints/_normalizer-option.rst.inc

.. include:: /reference/constraints/_payload-option.rst.inc

``version``
~~~~~~~~~~~

**type**: ``string`` **default**: ``4``

This determines exactly *how* the IP address is validated and can take one
of a variety of different values:

**All ranges**

``4``
    Validates for IPv4 addresses
``6``
    Validates for IPv6 addresses
``all``
    Validates all IP formats

**No private ranges**

``4_no_priv``
    Validates for IPv4 but without private IP ranges
``6_no_priv``
    Validates for IPv6 but without private IP ranges
``all_no_priv``
    Validates for all IP formats but without private IP ranges

**No reserved ranges**

``4_no_res``
    Validates for IPv4 but without reserved IP ranges
``6_no_res``
    Validates for IPv6 but without reserved IP ranges
``all_no_res``
    Validates for all IP formats but without reserved IP ranges

**Only public ranges**

``4_public``
    Validates for IPv4 but without private and reserved ranges
``6_public``
    Validates for IPv6 but without private and reserved ranges
``all_public``
    Validates for all IP formats but without private and reserved ranges

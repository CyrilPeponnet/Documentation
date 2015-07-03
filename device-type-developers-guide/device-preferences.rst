Preferences
===========

.. note::

    This documentation is incomplete. Until it is expanded, you are encouraged to look at other device-type handlers for example usage. The *SmartSense Multi* and *HomeSeer Multisensor*, available to browse via the "Device Type Templates" menu in the IDE, both use preferences.

Device type handlers can define preferences, similar to how SmartApps do. They are not the same, however.

When you add a device, in addition to the “name your device” field you could show other fields, and they’ll be editable by tapping the “preferences” tile in the device details. This is a fairly uncommon scenario, but would be handled by adding a preferences block to the metadata:

.. code-block:: groovy
    
    metadata {
        ...
        preferences {
           input "sampleInput", "number", title: "Sample Input Title", 
                  description: "This is the sample input.", defaultValue: 20, 
                  required: false, displayDuringSetup: true
        }
        ...
    }
    

Device preferences are limited to input elements, and do not support multiple pages or sections.

input
~~~~~

Allows the user to select or enter values to be used during execution of the device handler.

Inputs are the most commonly device settings. They can be used to customise devices properties (like zwave paramaters).

Valid input options:

*name*
    String - name of variable that will be created in this SmartApp to reference this input
*title*
    String - Title text of this element.
*description*
    String - Description of this element
*defaultValue*
    String - Default value of the input element
*multiple*
    Boolean - ``true`` to allow multiple values or ``false`` to allow only one value. Not valid for all input types.
*required*
    Boolean - ``true`` to require the selection of a device for this input or ``false`` to not require selection.
*submitOnChange*
    Boolean - ``true`` to force a page refresh after input selection or ``false`` to not refresh the page. This is useful
    when creating a dynamic input page.
*options*
    List - used in conjunction with the enum input type to specify the values the user can choose from. Example: ``options: ["choice 1", "choice 2", "choice 3"]``
    Or you an use map to show a string and store a value ``options: [[1:"item1]", [2:"item2"]]`` in this case the `defaultValue` must match "item1" or "item2".
*type*
    String - one of the names from the following table:

    ===========================  ===========================================================================================
    **Name**                     **Comment**
    ---------------------------  -------------------------------------------------------------------------------------------
    cacapability.capabilityName  Prompts for all the devices that match the specified capability.

                                 See the *Preferences Reference* column of the :ref:`capabilities_taxonomy`
                                 table for possible values.
    device.deviceTypeName        Prompts for all devices of the specified type.
    boolean                      A ``true`` or ``false`` value
    decimal                      A floating point number, i.e. one that can contain a decimal point
    email                        An email address
    enum                         One of a set of possible values. Use the *options* element to define the possible values.
    hub                          Prompts for the selection of a hub
    icon                         Prompts for the selection of an icon image
    number                       An integer number, i.e. one without decimal point
    password                     A password string. The value is obscured in the UI and encrypted before storage
    phone                        A phone number
    time                         A time of day. The value will be stored as a string in the Java `SimpleDateFormat <http://docs.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html>`__ (e.g., "2015-01-09T15:50:32.000-0600")
    text                         A text value
    ===========================  ===========================================================================================



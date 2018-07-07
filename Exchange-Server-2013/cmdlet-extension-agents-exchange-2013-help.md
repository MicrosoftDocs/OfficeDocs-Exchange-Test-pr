---
title: 'Cmdlet extension agents: Exchange 2013 Help'
TOCTitle: Cmdlet extension agents
ms:assetid: 0257790d-3988-46c3-8882-25ca11559e84
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dd335054(v=EXCHG.150)
ms:contentKeyID: 50117637
ms.date: 03/23/2018
mtps_version: v=EXCHG.150
---

# Cmdlet extension agents

 

_**Applies to:** Exchange Server 2013_


Cmdlet extension agents are components in Microsoft Exchange Server 2013 invoked by Exchange 2013 cmdlets when the cmdlets run. As the name implies, cmdlet extension agents extend the capabilities of the cmdlets that invoke them by assisting in processing data or performing additional actions based on the requirements of the cmdlet. Cmdlet extension agents are available on any server role.

Agents can modify, replace, or extend functionality of Exchange Management Shell cmdlets. An agent can provide a value for a required parameter that isn't provided on a command, override a value provided by a user, perform other actions outside of the cmdlet workflow while a cmdlet runs, and more.

For example, the **New-Mailbox** cmdlet accepts the *Database* parameter that specifies the mailbox database in which to create a new mailbox. In Microsoft Exchange Server 2007, if you don't specify the *Database* parameter when you run the **New-Mailbox** cmdlet, the command fails. However, in Exchange 2013, the **New-Mailbox** cmdlet invokes the `Mailbox Resources Management` agent when the cmdlet runs. If the *Database* parameter isn't specified, the `Mailbox Resources Management` agent automatically determines a suitable mailbox database on which to create the new mailbox and inserts that value into the *Database* parameter.

Cmdlet extension agents can only be invoked by Exchange 2013 and Microsoft Exchange Server 2010 cmdlets. Exchange 2007 cmdlets and cmdlets provided by other Microsoft and third-party products can't invoke cmdlet extension agents. Scripts also can't invoke cmdlet extension agents directly. However, if scripts contain Exchange 2013 cmdlets, those cmdlets continue to call the cmdlet extension agents.

Looking for management tasks related to cmdlet extension agents? See [Manage cmdlet extension agents](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Agent priority

The priority of an agent determines the order in which the agent is invoked while a cmdlet runs. An agent that has a higher priority, closer to zero, is invoked first. The priority of an agent becomes important when two or more agents attempt to set the value of the same property. The highest priority agent that attempts to set a property value succeeds, and all subsequent attempts to set the same property by lower priority agents are ignored. For example, if the **Name** property on an object is modified by an agent with a priority of 3 and another agent with a priority of 6 modifies the same object, the modification made by the agent with a priority of 6 is ignored.

If you want to use the `Scripting agent` to set the value of properties that might be set by other, higher priority agents, you have the following options:

  - Disable the agent that currently sets the property.

  - Set the `Scripting agent` to a priority higher than the existing agent you want to replace.

  - Keep the priorities of the agents the same and make sure that the script that runs under the `Scripting agent` respects the value provided by the other agents.


> [!WARNING]
> Changing the priority or replacing the functionality of a built-in agent is an advanced operation. Be sure that you completely understand the changes you're making.



For more information about changing the priority of an agent, see [Manage cmdlet extension agents](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Built-in agents

Exchange 2013 includes several agents that can be invoked when a cmdlet runs. The following table lists the agents, their order, and whether the agents are enabled by default. You can't add or remove agents to or from a server running Exchange 2013. However, you can use the `Scripting agent` to run Windows PowerShell scripts to extend the functionality of the cmdlets that use it. For more information about the `Scripting agent`, see the “Scripting agent” section later in this topic.

You can enable or disable most agents or change the priority of the agents if you want to replace the functionality of a specific agent with functionality you provide in a custom script that you call using the `Scripting agent`. However, some agents can’t be disabled. Agents that can’t be disabled are called *system agents* and have their *IsSystem* property set to `$True`. The following table provides information about Exchange 2013 cmdlet extension agents, including system agents.

The configuration for agents is stored at the organization level. When you enable or disable an agent, or set its priority, you set that agent configuration across every server in the organization. The exception is adding scripts to the `Scripting agent`. You must update the scripts on each server individually. For more information about configuring scripts for use with the `Scripting agent`, see the “Scripting agent” section later in this topic.


> [!WARNING]
> Changing the priority of agents, or enabling or disabling agents, can cause unintended effects if you don't completely understand what each agent does and how they interact with Exchange cmdlets. Before you change the configuration of any agent, be sure you fully understand the changes and results you want and that you verify that your custom script will work as intended.



### Exchange 2013 cmdlet extension agents

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Agent name</th>
<th>Priority</th>
<th>Enabled by default</th>
<th>System agent</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Admin Audit Log agent</code></p></td>
<td><p>255</p></td>
<td><p>True</p></td>
<td><p>Yes</p></td>
</tr>
<tr class="even">
<td><p><code>Scripting agent</code></p></td>
<td><p>6</p></td>
<td><p>False</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Resources Management agent</code></p></td>
<td><p>5</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><code>OAB Resources Management agent</code></p></td>
<td><p>4</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p><code>Query Base DN agent</code></p></td>
<td><p>3</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><code>Provisioning Policy agent</code></p></td>
<td><p>2</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p><code>Rus agent</code></p></td>
<td><p>1</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Creation Time agent</code></p></td>
<td><p>0</p></td>
<td><p>True</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


## Scripting agent

You can use the `Scripting agent` cmdlet extension agent in Exchange 2013 to insert your own scripting logic into the execution of Exchange cmdlets. Using the `Scripting agent`, you can add conditions, override values, and set up reporting.


> [!WARNING]
> When you enable the <CODE>Scripting agent</CODE> cmdlet extension agent, the agent is invoked every time a cmdlet is run on a server running Exchange 2013. This includes not only cmdlets run directly by you in the Exchange Management Shell, but also cmdlets run by Exchange services, and the Exchange Administration Center (EAC). We strongly recommend that you test your scripts and any changes you make to the configuration file before you copy your updated configuration file to your Exchange 2013 servers and enable the <CODE>Scripting agent</CODE> cmdlet extension agent.



Every time an Exchange cmdlet is run, the cmdlet invokes the `Scripting agent` cmdlet extension agent. When this agent is invoked, the cmdlet checks whether any scripts are configured to be invoked by the cmdlet. If a script should be run for a cmdlet, the cmdlet tries to invoke any APIs defined in the script. The following APIs are available and are invoked in the following order:

1.  **ProvisionDefaultProperties**   This API can be used to set values of properties on objects when they're created. When you set a value, that value is returned to the cmdlet and the cmdlet sets the value on the property. You can fill in values on properties if the user didn't specify a value, or you can override the value specified by the user. This API respects the values set by higher priority agents. The `Scripting agent` cmdlet extension agent won't overwrite the values set by higher priority agents.

2.  **UpdateAffectedIConfigurable**   This API can be used to set values of properties on objects after all other processing has been completed, but the `Validate` API hasn't yet been invoked. This API respects the values set by higher priority agents. The `Scripting agent` cmdlet extension agent won't overwrite the values set by higher priority agents.

3.  **Validate**   This API can be used to validate the values on an object's properties that are about to be set by the cmdlet. This API is called just before a cmdlet writes any data. You can configure validation checks that allow a cmdlet to either succeed or fail. If a cmdlet passes the validation checks in this API, the cmdlet is allowed to write the data. If the cmdlet fails the validation checks, it returns any errors defined in this API.

4.  **OnComplete**   This API is used after all cmdlet processing is complete. It can be used to perform post-processing tasks, such as writing data to an external database.


> [!NOTE]
> The <CODE>Scripting agent</CODE> cmdlet extension agent isn't invoked when cmdlets with the <CODE>Get</CODE> verb are run.



## Scripting agent configuration file

The `Scripting agent` configuration file contains all the scripts that you want the `Scripting agent` to run. Scripts in the configuration file are contained within XML tags that define the beginning and end of the script and various input parameters required to pass data to the script. Scripts are written using Windows PowerShell syntax. The configuration file is an XML file that uses the elements or attributes in the following table.

### Attributes of Scripting agent configuration file

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Element</th>
<th>Attribute</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Configuration</code></p></td>
<td><p>Not applicable</p></td>
<td><p>This element contains all the scripts that the <code>Scripting agent</code> cmdlet extension agent can run. The <code>Feature</code> tag is a child of this tag.</p>
<p>There is only one <code>Configuration</code> tag in the configuration file.</p></td>
</tr>
<tr class="even">
<td><p><code>Feature</code></p></td>
<td><p>Not applicable</p></td>
<td><p>This element contains a set of scripts that relate to a feature. Each script, defined in the <code>ApiCall</code> child tag, extends a specific part of the cmdlet execution pipeline. This tag contains the <code>Name</code> and <code>Cmdlets</code> attributes.</p>
<p>There can be multiple <code>Feature</code> tags under the <code>Configuration</code> tag.</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p><code>Name</code></p></td>
<td><p>This attribute contains the name of the feature. Use this attribute to help identify which feature is extended by the scripts contained within the tag.</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p><code>Cmdlets</code></p></td>
<td><p>This attribute contains a list of the Exchange cmdlets used by the set of scripts in this feature extension. You can specify multiple cmdlets by separating each cmdlet with a comma.</p></td>
</tr>
<tr class="odd">
<td><p><code>ApiCall</code></p></td>
<td><p>Not applicable</p></td>
<td><p>This element contains scripts that can extend a part of the cmdlet execution pipeline. Each script is defined by the API call name in the cmdlet execution pipeline it's extending. The following are the API names that can be extended:</p>
<ul>
<li><p><code>ProvisionDefaultProperties</code></p></li>
<li><p><code>UpdateAffectedIConfigurable</code></p></li>
<li><p><code>Validate</code></p></li>
<li><p><code>OnComplete</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p><code>Name</code></p></td>
<td><p>This attribute includes the name of the API call that's extending the cmdlet execution pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><code>Common</code></p></td>
<td><p>Not applicable</p></td>
<td><p>This element contains functions that can be used by any script in the configuration file.</p></td>
</tr>
</tbody>
</table>


Every Exchange 2013 server includes the file ScriptingAgentConfig.xml.sample in the \<*installation path*\>\\V15\\Bin\\CmdletExtensionAgents folder. This file must be renamed to ScriptingAgentConfig.xml on every Exchange 2013 server if you enable the Scripting Agent cmdlet extension agent. The sample configuration file contains sample scripts that you can use to help you understand how to add scripts to the configuration file.

After you add a script to the configuration file, or if you make a change to the configuration file, you must update the file on every Exchange 2013 server in your organization. This must be done to make sure that each server contains an up-to-date version of the scripts that the `Scripting Agent` cmdlet extension agent runs.

Some characters typically used in scripts also have a special meaning in XML. To use these characters in your script, use escape sequences. For example, the following characters use an escape sequence:

  - Instead of a greater than sign ( `>` ), use `&gt;`

  - Instead of a less than sign ( `<` ), use `$lt;`

  - Instead of an ampersand ( `&` ), use `&amp;`

## Enable the Scripting agent

The `Scripting agent` cmdlet extension agent is disabled by default. When you enable the `Scripting agent`, the agent is enabled for the entire Exchange 2013 organization. Before you enable the `Scripting agent`, verify that the `Scripting agent` configuration file has been correctly renamed and updated with your scripts on every Exchange 2013 server. You will receive an error message each time a cmdlet runs if you don't rename the configuration file correctly or copy a configuration file to this computer from another Exchange 2013 server.

To enable the `Scripting agent`, you must do the following:

1.  Rename the ScriptingAgentConfig.xml.sample file in **\<installation path\>\\V15\\Bin\\CmdletExtensionAgents** to ScriptingAgentConfig.xml on every Exchange 2013 server in your organization.
    

    > [!NOTE]
    > You can copy the configuration file from one Exchange 2013 server to other Exchange 2013 servers. Be sure you update the configuration file you want to copy before you copy it.



2.  Add your script to the renamed configuration file on every Exchange 2013 server in your organization.

3.  Enable the `Scripting agent` cmdlet extension agent. For more information about enabling cmdlet extension agents, see [Manage cmdlet extension agents](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Scripting Agent priority

By default, the `Scripting agent` cmdlet extension agent runs after every other agent, with the exception of the `Scripting agent` agent. If you want a script you created to replace an existing agent, you must either disable the other agent or change the priority of either agent so that the `Scripting agent` cmdlet extension agent runs first. For more information about how to disable or change the priority of agents, see [Manage cmdlet extension agents](manage-cmdlet-extension-agents-exchange-2013-help.md).


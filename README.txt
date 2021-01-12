###############
# Information #
###############
-Title: Dell EMC VMAX App for Splunk Enterprise
-App-on Version: 2.0.1
-Document Version: 2.0.0
-Date: 31st January 2018
-Vendor Products: Dell EMC VMAX3 and VMAX All-Flash
-Visible in Splunk Web: Yes

###########
# Contact #
###########
For any and all issues or queries, please contact vmax.splunk.support@emc.com.
Include as much information as possible about the issue, the Operating System
and Splunk versions, and associated log files.

-Response Time: Within 48hrs
-How we track issues: Internal Bug tracking system

###############################################
# Hours of Operation & Holidays Observed 2018 #
###############################################
All times are specific to Ireland (GMT+00:00)

Working Hours:
    Monday      : 09:00 - 17:00
    Tuesday     : 09:00 - 17:00
    Wednesday   : 09:00 - 17:00
    Thursday    : 09:00 - 17:00
    Friday      : 09:00 - 16:00
    Saturday    : Closed
    Sunday      : Closed

Holidays Observed 2018:
Date	    Weekday	    Holiday Name	        Holiday Type
Jan 1	    Monday	    New Year's Day	      National holiday
Mar 19	  Monday	    St. Patrick's Day     Observance
Mar 30	  Friday	    Good Friday	          Observance
Apr 1	    Sunday	    Easter	              Observance
Apr 2	    Monday	    Easter Monday	        National holiday
May 7	    Monday	    May Day	              National holiday
Jun 4	    Monday	    June Bank Holiday	    National holiday
Aug 6	    Monday	    August Bank Holiday	  National holiday
Oct 29	  Monday	    October Bank Holiday	National holiday
Dec 24	  Monday	    Christmas Eve	        Observance
Dec 25	  Tuesday	    Christmas Day	        National holiday
Dec 26	  Wednesday	  St. Stephen's Day	    National holiday
Dec 31	  Monday	    New Year's Eve	      Observance


###############################################
# About the VMAX Add-on for Splunk Enterprise #
###############################################
The Splunk App for Dell EMC VMAX allows a Splunk' Enterprise administrator to
take inventory, performance information, and summary information from VMAX
storage arrays through the VMAX Technical Add-on (TA) and present them in
pre-built dashboards, tables and time charts for in-depth analysis and
drill-downs to event.

Download the Splunk App for Dell EMC VMAX from Splunkbase.


#################
# Release Notes #
#################
Version 2.0.1 of the VMAX App is compatible with:
    -Splunk Platform: 6.4 and above
    -CIM: 4.6 and above
    -OS Platforms: Splunk compatible platforms
    -Vendor Hardware: Dell EMC VMAX3 and VMAX All-Flash
    -Vendor Software: Solutions Enabler 8.4.0.7 and newer
                      Unisphere for VMAX 8.4.0.10 and newer

The VMAX App for Splunk Enterprise contains dashboards which present data
captured from the following VMAX TA reporting levels:
    -VMAX (array level)
    -VMAX System Alerts
    -Storage Resource Pool
    -Storage Group
    -Director (FE/BE/RDF/IM/EDS)
    -Port
    -Port Group
    -Host
    -Initiator
    -Workload Planner (Compliance/Head room)


#######################################################
# VMAX App for Splunk Requirements and Considerations #
#######################################################
-Splunk Administrator Requirements
To install and configure the Splunk VMAX App, you must have admin privileges.

-Hardware & Software
As this app runs on Splunk Enterprise, all Splunk Enterprise system requirements
apply. In order for the Splunk app for VMAX to work correctly, the VMAX TA must
also be installed and configured in the environment in-advance of installing the
VMAX app. Install the VMAX app on search heads so it can run queries on the
indexes defined in the VMAX TA which contain the VMAX event data.

The VMAX App uses Splunk macros to shorten lengthy and frequent search queries.
By default, these queries use the Splunk default index as configured by the
user, typically this is the 'main' index but can be changed. If you store your
VMAX event data in a different index from the default index, or have distributed
your VMAX data across multiple indexes, you will need to configure these macros
to use the correct indexes in order for the app dashboards to work as intended.


#######################################################################
# Installation and Configuration Overview for the VMAX App for Splunk #
#######################################################################
As there are no dependencies required for the installation of the VMAX App for
Splunk, the set-up is completed from the Splunk Web UI and, if required,
associated VMAX App macro configuration file.

1. From your Splunk home screen, click the cog icon beside 'Apps' to navigate to
the 'Manage Apps' section.

2. Within the 'Manage Apps' section, click the button 'Install App from file'.

3. Click 'Choose File', select the VMAX App for Splunk, and click 'Upload'.

4. (OPTIONAL) If you have configured the VMAX TA for Splunk to index event data
in an index other than the default index you will need to reconfigure the VMAX
App macro configuration. Navigate to the installation directory of the VMAX App
for Splunk which contains all default configuration files:
# cd {splunk_dir}/etc/apps/Dell-EMC-app-VMAX/default

Copy macros.conf to the local directory in the App installation directory:
# cp macros.conf {splunk_dir}/etc/apps/Dell-EMC-app-VMAX/local

Edit the newly copied macros.conf so that each 'index=' key/value pair
represents the indexes in use in your environment. Each reporting level ingested
by the VMAX TA corresponds to a macro in macros.conf, so you will be able to set
different indexes for array level, host level, or alert level metrics for
example.

Example:
[vmax_array]
definition = index=main sourcetype=dellemc:vmax:rest reporting_level="Array"
Becomes:
[vmax_array]
definition = index=vmax_array sourcetype=dellemc:vmax:rest reporting_level="Array"

Once all the macros have been updated to reflect the indexes in use, save the
file and return to Splunk UI.

5. Once the VMAX App is added to Splunk you will be not be prompted to restart
Splunk to complete the installation, but it is advisable to restart Splunk
before using the App and also to apply any optional changes made in step 4.
Navigate to 'Settings > Server Controls', and click 'Restart now'. When Splunk
restarts, navigate back to the home screen and you will now see a dashboard
panel for the VMAX App.


###############################
# VMAX App Usage & Navigation #
###############################
Navigating throughout the VMAX App is done entirely through the menu featured at
the top of the screen when you open the VMAX App.

By default, the drop-down boxes in each dashboard will feature all the objects
available at that reporting level through the 'ALL' option. You can drill down
further by array ID and more depending on the dashboard you are within.

The default time-range for each dashboard time chart is last 24 hours. This time
can be changed by changing the time settings under 'Time Frame'. It works the
same as all other Splunk time range pickers.

It is important to note that not all panels within each dashboard are set to
represent data from the last 24 hours, most are set to present the most recent
and up to date information to the user. As a rule of thumb, only time charts in
the VMAX App dashboards reflect data from the time range specified in the time
range picker. All other panels, such as tables, single number panels, pie
charts etc., all represent the most-recent information up-to-date from the most
recent VMAX event data. If there is an issue with data collection and the data
is older than 10minutes old some of the panels may display a 'No Results Found'
message. To check this, check your VMAX TA logs to determine if data is still
being collected by the VMAX TA.


##############################################
# Source Type for the VMAX Add-on for Splunk #
##############################################
The VMAX TA provides the index-time and search-time knowledge for inventory,
performance metrics, and summary information. By default, all VMAX data is
indexed into the default Splunk index, this is the ‘main’ index unless changed
by the admin.

The source type used for the Splunk Add-on for VMAX is dellemc:vmax:rest. All
events are in key/value pair formats. All events have an assigned
'reporting_level' which indicates the level at which the event details, along with
the associated VMAX array ID & if reporting at lower levels, the object ID e.g.
Storage Group, Director, Host.

The add-on collects many different kinds of events for VMAX, including
performance, inventory, and summary metrics. Depending on the activity of the
Port Groups & Initiators in your environment, there may be events where there
are no performance metrics collected. This can be confirmed if there is a metric
present in the event named {reporting_level}_perf_details with a value of False
(where reporting_level is the reporting level of the event itself). For more
information see the section ‘Active vs. Inactive Object Performance Reporting’.


####################################################
# Active vs. Inactive Object Performance Reporting #
####################################################
To limit the amount of data collected and stored on a VMAX, only active Port
Groups, Hosts, and Initiators are reported against for performance metrics.
Inactivity is determined by no activity being recorded by performance monitors
for a specified amount of time. The VMAX TA ingests a wide range of metrics
across each of the reporting levels. To get detailed definitions of each of the
performance metrics see the ‘Performance Management’ section of the
‘Unisphere 8.4 Online Help’ guide available on support.emc.com

This is not enforced by Splunk but is the behaviour of the VMAX, recording zero
values for every Port Group, Host, and Initiator in an environment would very
quickly fill databases with useless data.

When the VMAX TA is collecting information on the Port Groups, Hosts, or
Initiators in your environment, it will first obtain a list of all objects for
each reporting level. Using this list, calls will be to Unisphere for
performance metrics for each, if an object is inactive, no performance metrics
will be returned. This inactivity is reflected in the VMAX events through the
key/value pairs below.

{reporting_level}_perf_details: false
{reporting_level}_perf_message: No active {reporting_level} performance data
                                available


############################################
# Troubleshooting the VMAX App for Splunk #
############################################
The VMAX App for Splunk has been designed in such a way that there is little or
no user interaction required in order to get it running in the environment. The
only use-case for when manual configuration is required is when indexes are used
by the VMAX TA which differ from the default Splunk index (see installation &
configuration section above for more info).

If you are having issues with the macros in your VMAX App, check the indexes
configured for use by each of the VMAX TA data inputs, the indexes specified by
each input should match those used by the VMAX App in the macros.conf
configuration file. If these do match and everything appears to be correct,
restart Splunk to ensure that the changes have been applied and settings are
read from the VMAX App's local directory.

As the VMAX App only takes the data ingested by the VMAX TA and presents it in
dasboards populated with various panels, there is no other VMAX App settings or
areas which could cause issues to appear within the App. If you are facing any
issues in the VMAX App and the macros are configured correctly, the next place
to troubleshoot is in the VMAX TA itself. For information on troubleshooting the
VMAX TA, please see the 'Troubleshooting' section in the VMAX TA user-guide.


################
# Known Issues #
################
-VMAX Alerts
When requesting VMAX alert information from the Unisphere REST API through the
/system/alert endpoints there is no key/value pairs for the array and object ID.
When the event is processed in the VMAX TA, the alert description is parsed and
if an array or object ID is present, it is added before the data is indexed in
Splunk. At present, most information can be parsed from the description but this
does not always work.

An example of not being able to parse the array/object info from an alert is
with array metadata usage. Using the REST API there is no IDs associated with
the alert so unless the user reverts to Unisphere manually there is no way they
can know what array the alert belongs to.

The impact of this in the VMAX TA is that when 'Collect VMAX only metrics' is
enabled, certain alerts which do not have the array/object info in the alert
description will not be ingested into Splunk. This is because this option uses
the array ID key/value pair to determine if it is related to the VMAX ID
specified in the data input.

It must be noted however, that the data for which the alert describes can be
viewed within the various dashboards of the VMAX App for Splunk. For example,
the array metadata usage percentage is featured as a time chart in the VMAX
dashboard. This is because for each of the reporting levels, every possible
piece of information pertaining to each reporting levels' objects is retrieved
from Unisphere.

If 'Collect VMAX only metrics' is left disabled, all system alerts from the
instance of Unisphere specified in the VMAX data input will be ingested into
Splunk. This also means that any system alerts for other arrays which are not
added as data inputs, but present in that instance of Unisphere associated with
the data input are ingested into Splunk.


###########
# Contact #
###########
For any and all issues or queries, please contact vmax.splunk.support@emc.com.
Include as much information as possible about the issue, the Operating System
and Splunk versions, and associated log files listed in the troubleshooting
section.

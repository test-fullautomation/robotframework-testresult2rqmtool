.. Copyright 2020-2022 Robert Bosch GmbH

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.

RobotResults2RQM
================

Table of Contents
-----------------

-  `Getting Started <#getting-started>`__

   -  `How to install <#how-to-install>`__
-  `Usage <#usage>`__
-  `Example <#example>`__
-  `Contribution <#contribution>`__
-  `Sourcecode Documentation <#documentation>`__
-  `Feedback <#feedback>`__
-  `About <#about>`__

   -  `Maintainers <#maintainers>`__
   -  `Contributors <#contributors>`__
   -  `License <#license>`__
   
Getting Started
---------------

RobotResults2RQM_ is the tool that helps to import Robot Framework results 
(***.xml** format) to `IBM® Rational® Quality Manager`_ - RQM.

RobotResults2RQM_ tool is operating system independent and only works with 
Python 3.

How to install
~~~~~~~~~~~~~~
RobotResults2RQM is not available on PyPI_ now.

But you can install this package directly from Github repository as below:

::

   pip install git+https://github.com/test-fullautomation/robotframework-testresult2rqmtool.git

Or you can clone sourcecode to your local directory then install this package 
with below steps:

::

   git clone https://github.com/test-fullautomation/robotframework-testresult2rqmtool.git
   cd robotframework-testresult2rqmtool
   python setup.py install

After succesful installation, the executable file **RobotResults2RQM** 
will be available (under *Scripts* folder of python on Windows 
and *~/.local/bin/* folder on Linux).

In case above location is added to **PATH** environment variable 
then you can run it directly as operation system's command.

Usage
-----

RobotResults2RQM_ tool requires the robot ``output.xml`` result file(s) which will 
be imported, RQM information(e.g. host url, project, ...) and user 
credential(user name and password) to interact with RQM resources.

Try with below command to get tools's uage
::

   RobotResults2RQM -h


The usage should be showed as below:
::

   usage: RobotResults2RQM (XMLoutput to RQM importer) [-h] [-v] [-recursive] [-createmissing] [-updatetestcase] [-dryrun]
                                                      outputfile host project user password testplan

   RobotResults2RQM imports XML output files (default: output.xml) generated by the Robot Framework into a IBM Rational Quality Manager.        

   positional arguments:
   outputfile       absolute or relative path to the output file or directory with output files to be imported.
   host             RQM host url.
   project          project on RQM.
   user             user for RQM login.
   password         password for RQM login.
   testplan         testplan ID for this execution.

   optional arguments:
   -h, --help       show this help message and exit
   -v               Version of the RobotResults2RQM importer.
   -recursive       if set, then the path is searched recursively for log files to be imported.
   -createmissing   if set, then all testcases without fcid are created when importing.
   -updatetestcase  if set, then testcase information on RQM will be updated bases on robot testfile.
   -dryrun          if set, then just show what would be done.


The below command is simple usage witth all required argurments to import 
robot results into RQM:
::

   RobotResults2RQM <outputfile> <host> <project> <user> <password> <testplan>

Besides the executable file, you can also run tool as a python module
::

   python -m RobotResults2RQM <outputfile> <host> <project> <user> <password> <testplan>


Example
-------
In order the import the robot result(s) to RQM, we need the ``output.xml`` result file.

So, firslty execute the robot testcase(s) to get the ``output.xml`` result file.

Sample robot testcase which contains neccessary information for importing into RQM:
::

   *** Settings ***
   Metadata   project      ROBFW             # Test Environment
   Metadata   version_sw   SW_VERSION_0.1    # Build Record
   Metadata   component    Import_Tools      # Component - is used for test case
   Metadata   machine      %{COMPUTERNAME}   # Hostname
   Metadata   team-area    Internet Team RQM  # team-area (case-sensitive)

   *** Test Cases ***
   Testcase 01
      [Documentation]   This test is traceable with provided tcid  
      [Tags]   TCID-1001   FID-112   FID-111    robotfile-https://github.com/test-fullautomation
      Log      This is Testcase 01

   Testcase 02
      [Documentation]  This new testcase will be created if -createmissing argument 
                  ...  is provided when importing
      [Tags]   FID-113  robotfile-https://github.com/test-fullautomation
      Log      This is Testcase 02

After getting ``output.xml`` result file, try with below sample command to 
import that result into testplan ID ``720`` of ``CMD`` project which is hosted 
at ``https://rb-alm-20-p.de.bosch.com`` 
::

   RobotResults2RQM output.xml https://rb-alm-20-p.de.bosch.com CMD test_user test_pw 720

Then, open RQM with your favourite browser and you will see that the test case 
execution records and their results are imported in the given testplan ID.

Contribution
------------
We are always searching support and you are cordially invited to help to improve 
RobotResults2RQM_ tool.

Sourcecode Documentation
------------------------
To understand more detail about the tool's features and how resources are mapped
between Robot results and RQM, please refer to 
`RobotResults2RQM tool’s Documentation`_.


Feedback
--------
Please feel free to give any feedback to us via

Email to: `Robot Framework Support Group`_

Issue tracking: `RobotResults2RQM Issues`_

About
-----

Maintainers
~~~~~~~~~~~
`Thomas Pollerspöck`_

`Tran Duy Ngoan`_

Contributors
~~~~~~~~~~~~

`Nguyen Huynh Tri Cuong`_

`Mai Dinh Nam Son`_

`Tran Hoang Nguyen`_

`Holger Queckenstedt`_


License
~~~~~~~

Copyright 2020-2022 Robert Bosch GmbH

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    |License: Apache v2|

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


.. |License: Apache v2| image:: https://img.shields.io/pypi/l/robotframework.svg
   :target: http://www.apache.org/licenses/LICENSE-2.0.html
.. _IBM® Rational® Quality Manager: https://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.2/com.ibm.rational.test.qm.doc/topics/c_qm_overview.html
.. _PyPI: https://pypi.org/
.. _Robot Framework Support Group: mailto:RobotFrameworkSupportGroup@bcn.bosch.com
.. _Thomas Pollerspöck: mailto:Thomas.Pollerspoeck@de.bosch.com
.. _Tran Duy Ngoan: mailto:Ngoan.TranDuy@vn.bosch.com
.. _Nguyen Huynh Tri Cuong: mailto:Cuong.NguyenHuynhTri@vn.bosch.com
.. _Mai Dinh Nam Son: mailto:Son.MaiDinhNam@vn.bosch.com
.. _Tran Hoang Nguyen: mailto:Nguyen.TranHoang@vn.bosch.com
.. _Holger Queckenstedt: mailto:Holger.Queckenstedt@de.bosch.com
.. _RobotResults2RQM: https://github.com/test-fullautomation/robotframework-testresult2rqmtool
.. _RobotResults2RQM Issues: https://github.com/test-fullautomation/robotframework-testresult2rqmtool/issues
.. _RobotResults2RQM tool’s Documentation: https://github.com/test-fullautomation/robotframework-testresult2rqmtool/blob/develop/RobotResults2RQM/RobotResults2RQM.pdf

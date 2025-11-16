# MyProject001

<html>
<head>
  <meta charset="UTF-8">
  <title>Milestone Past Due Notice</title>
</head>
<body style="margin:0; padding:0; background-color:#ffffff;">
  <table width="70%" cellpadding="0" cellspacing="0" border="0" align="center" style="margin:auto;background-color:#ffffff; font-family: Arial, Helvetica, sans-serif;">
<tr>
      <td width="50%" style="font-size:18px; color:#333333; padding-top:18px">
        <img src="variable" width="300px" />
      </td>
      
    </tr>
    <tr>
      <td width="50%" style="font-size:18px; color:#333333; padding-top:18px">
        Environmental Remediation
      </td>
      <td width="50%"  style="font-size:18px; color:#333333; padding-top:18px" align="right">formatDateTime(utcNow(), 'MMMM d, yyyy')
</td>
    </tr>
	 <tr>
      <td width="100%"  colspan="2" style="font-size:24px; color:#333333; padding:0px 0px">
       <hr>
      </td>
    </tr>
    <tr>
      <td colspan="2" style="font-size:22px; font-weight:bold; color:#222222; padding-bottom:20px; padding-top:6px;">
        A Milestone Assigned To You Is 
        <span style="color:#d8000c; font-weight:bold;">Past Due</span>
      </td>
    </tr>
    <tr>
      <td colspan="2" style="font-size:15px; color:#222222; padding-bottom:20px;">
        If this milestone has been completed, please follow the View Task link below to update <b>STATUS:taskstatus </b>
      </td>
    </tr>
    <tr>
      <td colspan="2" style="font-size:18px; font-weight:bold; color:#222222; font-style:italic; padding-top:20px; padding-bottom:20px;">
        Milestone Name: <span style="font-style:italic;">Title</span>
      </td>
    </tr>
    <tr style="padding-bottom:20px">
      <td colspan="2" style="font-size:14px; color:#333333; padding-bottom:5px;">
        Program: <b>@{triggerOutputs()?['body/Program']}</b>
      </td>
    </tr>
    <tr>
      <td colspan="2" style="font-size:14px; color:#333333; padding-bottom:5px;">
        Project: <b>@{triggerOutputs()?['body/Project']}</b>
      </td>
</tr>
    <tr>
      <td colspan="2" style="padding-top:20px">
        <table cellpadding="0" cellspacing="0" border="0" width="30%" style="background-color:#f5f5f5; border-radius:5px; padding:12px; margin-bottom:18px;">
          <tr>
            <td style="font-size:16px; color:#367b35; font-weight:bold; padding-top:8px; padding-bottom:2px;">
              Start Date:
            </td>
            <td style="font-size:15px; color:#222222; padding-left:8px; padding-top:8px; padding-bottom:2px;">
              @{formatDateTime(triggerOutputs()?['body/StartDate'], 'M/d/yyyy')}
            </td>
          </tr>
          <tr>
            <td style="font-size:16px; color:#367b35; font-weight:bold; padding-top:4px; padding-bottom:8px;">
              Due Date:
            </td>
            <td style="font-size:15px; color:#222222; padding-left:8px; padding-top:4px; padding-bottom:8px;">
            @{formatDateTime(triggerOutputs()?['body/TaskDueDate'], 'MMMM d, yyyy')}
            </td>
          </tr>
        </table>
     </td>
    </tr>
    <tr>
      <td width="50%" style="padding-bottom:6px;">
        <a href="@{triggerOutputs()?['body/{Link}']}" style=" color:#367b35; text-decoration:underline; font-weight:bold; font-size:15px;">Click Here To View Milestone</a>
      </td>
	  <td width="50%" style="padding-top:10px; padding-bottom:18px;" align="right">
        <a href="@{variables('var_SiteURL')}" style="color:#367b35;text-decoration:underline; font-weight:bold; font-size:15px;">Click Here To Go To Program Site</a>
      </td>
    </tr>
    <tr>
      
    </tr>
  </table>
</body>
</html>

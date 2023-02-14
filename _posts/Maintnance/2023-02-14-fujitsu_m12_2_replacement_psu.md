---
title : How to replace PSU in Fujitsu M12-2/M12-2S Server
date : 2023-02-14 01:00:00 + 0900
categories : [SERVER, UNIX]
tags : [oracle, fujitsu, sparc, m12-2, m12-2s, replacement, psu]
render_with_liquid: false
---


# <b>How to Replace PSU in Fujitsu M12-2/M12-2S Server 

> TIME ESTIMATE: 20mins
{: .prompt-tip }


> <b> PSU 교체 시 주의 사항 </b>
*  PSU 교체 전 정전기 방지 팔찌를 착용 및 접지 후 작업 진행
* PSU 교체 대상이 여러개일 경우 하나 씩 교체 
* PSU 교체 시 PSU가 반대로 삽입되어 BPU(Backplain Unit) 또는 PSUBP(Power Supply Backplain Unit)이 손상 되지않도록 주의하여 작업한다.
{: .prompt-warning }


<br>
## <b>Releasing the PSU

### 1. Log in to the XSCF shell.
```

XSCF>

```

### 2. Execute the replacefru command to display the maintenance menu.
```

XSCF> replacefru

```


### 3. With a number key, select the chassis requiring maintenance.

### 4. With a number key, select the CRU requiring maintenance.
Example: PSU (Power Supply Unit).


### 5. With a number key, select the faulty CRU.
Example: /BB#x/PSU#x.
	

### 6. Confirm that the selected CRU is displayed, and then enter "r".

### 7. Remove the PSU to be replaced, as instructed in the onscreen message.
> Do not enter "f" until you mount the replacement PSU.
{: .prompt-warning }  

  
<br>  
## <b>Removing a PSU

### 1. Remove the power cord.
   Remove the power cord from the cable clamp of the PSU requiring maintenance and then remove the power cord from the PSU.

### 2. Pull down the handle of the PSU.

### 3. Remove the PSU from the server main unit.

> 
Note - For your safety, remove the power cord from the PSU before removing the PSU from
the server main unit.
{: .prompt-info }


<br>
## <b>Installing a PSU

### 1. Install a PSU to the server main unit.
   Insert the PSU into the server main unit, push it until its latch locks, and then push up the handle of the PSU.
> 
Note - When inserting the PSU into the server main unit, make sure that the PSU power
outlet is on the left side.
{: .prompt-info }

### 2. Install the power cord to the PSU.
   Connect the power cord to the PSU and then secure the cord with the cable clamp.


<br> 
## <b>Incorporating the PSU

### 1. Mount the replacement PSU, and connect the power cord to it. After connecting the power cord, wait for at least 10 seconds.

### 2. Check the result of incorporating the PSU.
Check that Normal is displayed under Status. Then, enter "f" to finish the maintenance of the PSU.

>
Note -If the displayed status is abnormal (Degrade or Fault), finish the maintenance of
the PSU and return to the maintenance start screen. Perform maintenance on the
PSU again, and check whether the PSU is correctly mounted.
{: .prompt-info }

### 3. End the replacefru command.
When the maintenance start screen appears, enter "c" to end the replacefru command.

- WHAT ACTIONS ARE REQUIRED TO RETURN THE SYSTEM TO AN OPERATIONAL STATE?:

Check the PSU status after maintenance

```
XSCF> showstatus
XSCF> showhardconf -M
``` 

<br> 

## <b> Referances </b>

- _Oracle Support Document 2234743.1 (Fujitsu M12-2/M12-2S: How to Replace a Power Supply (PSU) [VCAP]_  <https://support.oracle.com/epmos/faces/DocumentDisplay?id=2234743.1>


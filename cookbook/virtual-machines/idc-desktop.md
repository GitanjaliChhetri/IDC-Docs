# 3D Slicer desktop VM

{% hint style="info" %}
In order to follow these instructions, you will need to have a project that has billing enabled. Please follow the instructions in [getting-started-with-gcp.md](../../introduction/getting-started-with-gcp.md "mention") to set up billing.&#x20;
{% endhint %}

You can launch a VM in your project with a command like this in your local terminal (replace `vm-name` with a name for your machine):

{% hint style="warning" %}
The current image we created requires GPU accelerator! If you do not specify the accelerator in the command below, you will not be able to access the machine!
{% endhint %}

```
export VMNAME=vm-name
gcloud compute instances create ${VMNAME} \
  --machine-type=n1-standard-8 \
  --accelerator=type=nvidia-tesla-k80,count=1 \
  --image-family=slicer \
  --image-project=idc-sandbox-000 \
  --boot-disk-size=200GB \
  --boot-disk-type=pd-balanced \
  --maintenance-policy=TERMINATE
```

Once it boots in about 90 seconds you can type:

```
gcloud compute ssh ${VMNAME} -- -L 6080:localhost:6080
```

Then you can open `http://localhost:6080/vnc.html?autoconnect=true` to get to your desktop.

Note that this effort is a work in progress with a minimal desktop environment. Further refinement is expected and community contributions would be welcome! A description of the background and possible evolution of this work is [in this document](https://docs.google.com/document/d/1jfHqjS7Fer7Lhqea5bjyown0b04AsqeOhIBY2gWUDO4/edit).

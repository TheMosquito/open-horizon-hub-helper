# open-horizon-hub-helper

How to setup your own Open Horizon Management Hub (using the All-In-One). Please note that the All-In-One deployment is not suitable for production use. It was conceived as a tool for Open Horizon developers. Nevertheless, I use it to manage containerized applications on edge nodes in my home. All of my edge nodes are stand-alone Linux hosts running either docker or podman. Of course, you can manage containerized applications on Kubernetes with this All-In-One Management Hub too, if you wish. The hub you create here fully supporrts stand-alone Linux hosts or Kubernmetes clusters. But I do not have any Kubernetes clusters in my home. So i don't have any cluster type nodes in my Management Hub.

These are hints to myself mostly, because I always have trouble getting this right.

The HOW_TO... recipes I offer here are based on the All-In-One tools, described here:
   [https://github.com/open-horizon/devops/tree/master/mgmt-hub](https://github.com/open-horizon/devops/tree/master/mgmt-hub)

I love the All-In-One. It makes Open Horizon usable for my personal projects. Unfortunately though the All-In-One has a problem common to many of the Open Horizon tools. It does lots of things by default that no normal users want, including installing a local agent on the same host as the Managment Hub. That is something I believe nobody would do in production. I believe it is not useful except possibly for some of the developers of Open Horizon. Unfortunately after that it goes even further and registers that local Agent to run a useless workload (`ibm.helloworld`). By passing flags to the Open Horizon scripts you can avoid doing these things, but that is risky in my opinion (I have had problems when I have done this). So I feel it is safer to let the scripts do what they want by default, and then manually undo the parts you don't want. So that's what my HOW_TO... recipes do. It takes a little longer this way but for me this always works. The net result is a Management Hub with a dormant (unregistered) Agent, which is mostly harmless, and safe.

Also noteworthy is that the All-In-One Management Hub, by default, **binds only to the host loopback interface**!! This of course means that no edge nodes can connect to it at all!! So my `HOW_TO_SETUP_AN_OPEN_HORIZON_HUB` recipe tells you to install the All-In-One using the default settings, then take it down, then change the bind address to the host's LAN IP address (where edge nodes can reach it), then you will bring it back up, and then finally it will also have you unregister the spurious `ibm.helloworld` workload. Phew! Sounds like a lot but it's just a few steps and takes just minutes to complete.

Once you have done all of the steps in my `HOW_TO_SETUP_AN_OPEN_HORIZON_HUB` recipe, you can start registering edge nodes.

Unfortunately the edge node agent installation process also installs this spuriouus `ibm.helloworld` workload. So my HOW_TO_SETUP_DEVICE_NODES recipe gets you to undo that. After those steps are complete yoou can go ahead and register the edge node normally using a node policy or a deployment pattern.

Also note that the All-In-One Management Hub fully supports SDO. Details on that are here: [https://github.com/open-horizon/SDO-support](https://github.com/open-horizon/SDO-support).

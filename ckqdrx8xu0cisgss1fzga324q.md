## What is edge computing and why does it matter?

There are many good definitions of What?, So I’ll stress more on the **WHY?** part

**What is edge computing ?**
Edge computing is a networking philosophy focused on bringing computing as close to the source of data as possible in order to reduce latency and bandwidth use.

**How does it work ?**
It works by running fewer processes in the  [cloud](https://www.cloudflare.com/en-gb/learning/cloud/what-is-the-cloud) and moving those processes to local places, such as on a user’s computer, an [IoT device](https://www.cloudflare.com/en-gb/learning/ddos/glossary/internet-of-things-iot), or an [edge server](https://www.cloudflare.com/en-gb/learning/cdn/glossary/edge-server). Bringing computation to the network’s edge minimizes the amount of long-distance communication that has to happen between a [client and server](https://www.cloudflare.com/en-gb/learning/serverless/glossary/client-side-vs-server-side).

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624711629767/KBY0_Gegt.png)

**Why is it the next big thing?**
So the cloud era gains traction because of being server-less and how easy and cheap it was to deploy and manage an application. This was true a few years ago. Fast forward to today, companies now actually spending millions on the breed of engineers(DevOps) to maintain [**cloud orchestration**](https://searchitoperations.techtarget.com/definition/cloud-orchestrator)**.**
The process has become more complex already and we now have interconnected devices generating billions of TB of data each day.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624711678312/S69EIpClU.png)

if you know any infrastructure engineer or DevOps guy ask him about **cold start issues**, klunky orchestration, etc.
We need Edge computing because the cloud won’t keep up. Today's hyperscale cloud data centers are modern marvels, but they're a bad fit for the era of connected things. The scale of connected devices and the growth of data generated in this next technological phase is almost unimaginable. There isn't enough bandwidth on the planet to haul the volume of usable edge data back to the cloud, and there never will be. Cloud giants know this, hence big companies are coming to their edge versions of the cloud like K8s(Google), aws Wavelength(Amazon), etc.

**Use case?**
Applications one can think of as of now are IOT devices, AR/ VR based applications, Drone, Automatic cars, etc.

*Imagine an automatic drone flying above on streets and someone gave instructions to turn left, instead of processing the instructions with the cloud, it is going to communicate and process data with someone’s car running under it locally because it has compute power required near to its location. We will have entire future smart cities built on it. Boundaries will be pushed and AI, ML applications will have a robust network, I mean possibilities are endless and what it will do is **not yet known**.*

**References:**

[What is Edge Computing?](https://edjx.io/what-is-edge-computing)

[EDJX and Atrius Industries Partner with Autonomy Institute to Deliver Autonomous Solutions at the Edge](https://edjx.io/edjx-autonomy-pr) 


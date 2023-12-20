# 300 - Building Our Application

## 100 - How to use for a Gitpod workspace

**NOTE**: If you do not have a ```.gitpod.yml``` at the **root** of your repository, run ```gp init -i``` in your terminal to create one.

Put the following line in your ```.gitpod.yml```:

```
image: gitpod/workspace-full-vnc
```
.gitpod.yml

Lastly, [see it in action!](https://www.gitpod.io/docs/introduction/learn-gitpod/gitpod-yaml#see-it-in-action)

## 200 - Details

🖥 This image is mainly useful for GUI application development where you need a display server.

🔋 It's built on top of [workspace-full](https://hub.docker.com/r/gitpod/workspace-full), it additionally contains:

- tigervnc server
- noVNC viewer
- google-chrome
- xfce4 desktop environment
- [gp-vncsession](https://github.com/gitpod-io/workspace-images/blob/axonasif/add_docs/chunks/tool-vnc/gp-vncsession) script

Every time a Gitpod workspace is started, `gp-vncsession` script is executed from the workspace [`.bashrc`](https://github.com/gitpod-io/workspace-images/blob/axonasif/add_docs/chunks/tool-vnc/Dockerfile#L26) file.

The web VNC client (i.e. noVNC) can be accessed by opening the preview of port `6080`. (e.g. `gp preview "$(gp url 6080)" --external`)

If you wish to use a local VNC client such as [RealVNC](https://www.realvnc.com/en/connect/download/viewer/) or tigervnc-viewer, you would need to forward the workspace ports to your localhost[^1] and connect to `localhost:5900`.

This image could be used for:

- E2E testing requires a GUI based browser. (cypress, playwright, selenium and etc.)
- Some CLIs try to launch browser auth by default, it could help in that.
- GUI application development. Or just simply to run any Linux GUI application.

You can set the VNC server display resolution through the `TIGERVNC_GEOMETRY` variable. So for example, you could have such a custom dockerfile:

```dockerfile
FROM gitpod/workspace-full-vnc

ENV TIGERVNC_GEOMETRY=1280x800
```

For more details, check the [Dockerfile](https://github.com/gitpod-io/workspace-images/blob/axonasif/add_docs/chunks/tool-vnc/Dockerfile)

## 300 - To be aware of

- There is no GPU acceleration. It's completely software rendered.
- Some complex 3D applications might crash.

## 400 - Learn more

- Docs:
    - https://www.gitpod.io/docs/introduction/languages/python#gui-applications-with-wxpython
- Blogs:
    - https://www.gitpod.io/blog/native-ui-with-vnc

[^1]: https://www.gitpod.io/docs/configure/workspaces/ports#port-forwarding

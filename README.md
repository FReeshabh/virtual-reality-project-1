# Virtual Reality Project 1 - Rishabh Tewari
This project is an individual project on creating a human scale scene, on how Covid 19 affected us. When opening up the project, we'll be transported to a *magical* 'Void' scene, with two transport orbs, for a pre-covid scene, and a post-covid (present) scene. 

The pre-covid scene showcases 'you' out and around in the real world, with other people, foxes, cars, etc. (and martial artists fighting!) The post covid scene transports us to a room (modelled after mine) where we are trapped, with interactive elements, and elements from the start of quarantine time (such as toilet paper).

You can also watch a video demo here by clicking on the image below

![Youtube Link](https://img.youtube.com/vi/CMYZBXiZqtQ/0.jpg)

You can view the live demo [here](https://freeshabh.github.io/virtual-reality-project-1/)


## Description
When the application starts we're transported to an empty area with two transport orbs. These two transport links are in fact links to the respective covid, and pre-covid scenes created with Aframe. The user needs to point their camera cursor at the orb that they want to explore and click. This will load in the new scene.
![Image of the initial void area with the two orbs](assets/img/pic1-void.png)

**Time to explore the pre-Covid-19 times area**

For our initial purposes, let's explore the pre-covid scenes. Upon entering the pre covid area we're greeted with this initial scene.

![Pre-Covid Scene 1](assets/img/pic2-precovid-1.png)

Moving our camera around a little, we can see there's more to this scene.

![Pre-Covid Scene 2](assets/img/pic3-precovid-2.png)

This `<a-scene>` is full of animated characters walking, fighting, and just relaxing in the wind. There's also a simulated pond, which is a result of a modified version of the ocean-plane.js file that I found on [glitch](https://glitch.com/edit/#!/acute-proximal-dog)

This pre-covid scene has models that you can read about [here](#pre-covid-situation). This scene represents how us and the world were before the pandemic, with people walking around, and being together. 

**About the water area**
This code was modified from this project I found on [glitch](https://glitch.com/edit/#!/acute-proximal-dog)

```
AFRAME.registerComponent('wobble-normal', {
	schema: {},
	tick: function (t) {
		if (!this.el.components.material.material.normalMap) return;
		this.el.components.material.material.normalMap.offset.x += 0.0001 * Math.sin(t/10000);
		this.el.components.material.material.normalMap.offset.y += 0.0001 * Math.cos(t/8000);
		this.el.components.material.material.normalScale.x = 0.5 + 0.5 * Math.cos(t/1000);
		this.el.components.material.material.normalScale.x = 0.5 + 0.5 * Math.sin(t/1200);
	}
})

AFRAME.registerPrimitive('a-ocean-plane', {
	defaultComponents: {
		geometry: {
            primitive: 'circle',
            radius:'20'

		},
		rotation: '-90 0 0',
		material: {
			shader: 'standard',
			color: '#8ab39f',
			metalness: 1,
			roughness: 0.2,
			normalMap: 'url(https://raw.githubusercontent.com/mrdoob/three.js/dev/examples/textures/waternormals.jpg)',
			normalTextureRepeat: '50 50',
			normalTextureOffset: '0 0',
			normalScale: '0.5 0.5',
			opacity: 1.0
		},
		'wobble-normal': {}
	},
});

```

There's full sized houses that the user can explore, and walk around to look at the floating cube which changes it's color from red to blue, when the user points the cursor at it. There's also an orbiting orb in the sky for good luck! To navigate to different areas of the application, the user can click on the transport orb which will transport us back to the *magical* Void area.

**Time to explore the Covid-19 times (present) area**

After transporting to the Covid-19 times area from the *magical* Void area. We're greeted with this initial scene.

![Covid scene 1](assets/img/pic4-postcovid.png)

We move the camera a bit to see what else is in the room

![Covid scene 2](assets/img/pic5postcovid.png)

This `<a-scene>` has interactable objects such as duck with a rather unsuited sound effect, an opening/closing door, and an adjustable light switch. Along with all these interactable objects, this scene also features 3D models that I designed myself! You can view these *made by me* models [here](#self-made-models-1), to view the all the models and textures used in this scene, go [here](#post-covid-present-situation).

There's a few easter eggs in the models made and imported. Features such as the toilet paper craze, which was a feature at the start of the pandemic, and my thoughts on VR at the present, and the cool Darth Vader model (made by me :)) 

**About the room**

The room component in the post covid scene did not use primitives, but used Aframe's room component that can be found [here](https://github.com/omgitsraven/aframe-room-component). 

```
<rw-room position="0 1 0" material="color:#C5EAFA; src:url(assets/wall.jpg); repeat: 2 2">
    <rw-ceiling position="0 0 0" material="color:#FFF; src:url(assets/ceiling.jpg); repeat:50 50"></rw-ceiling>
    <rw-floor position="0 0 0" material="src:url(assets/floor.png); repeat: 2 2"></rw-floor>
    <rw-wall position="6 0 0" height="3"></rw-wall>
	<rw-wall position="4 0 6" height="3"></rw-wall>
	<rw-wall position="0 0 6" height="3"></rw-wall>
	<rw-wall position="0 0 0" height="3">
        <rw-doorhole id="holeA"></rw-doorhole>
  		<rw-doorlink from="#holeA" to="#holeB" position="2.5 0 0"></rw-doorlink>
	</rw-wall>
  </rw-room>
<rw-room position="0 0 -3" outside="true">
	<rw-wall position=" 1 0  1" material="color:#877">
		<rw-doorhole id="holeB"></rw-doorhole>
	</rw-wall>
  </rw-room>
```

In hindsight, using simple primitives for the room would have sufficed, and would have probably been easier. However, I originally planned a bunch of rooms connected to each other until I realized that I live by myself in my own room, and have spent most of quarantine that way.

**The interactive door**

The code was originally modified from [mBhakta95'swork](https://github.com/mBhakta95/Virtual-Reality). This little script is the whole reason this door can close.

![closed door](assets/img/pic6-closeddoor.png)

<p align="center">Closed Door</p>

![open door](assets/img/pic7opendoor.png)

<p align="center">Open Door</p>

```
<script>
    var isOpened = false;
    var isClosed = true;
    function openDoor() {
        var my_door = document.querySelector('#OnlyDoor');
        if (isClosed) {
            my_door.setAttribute('rotation', "0 270 0");
            isOpened = true;
            isClosed = false;
        } else {
            my_door.setAttribute('rotation', "0 360 0");
            isOpened = false;
            isClosed = true;
        }
    }
</script>
```

**The light switch**

Here's 4 pictures comparing the brightness adjusted by the light switch.

![Different light levels](assets/img/pic-11-light4.png)

![Different light levels](assets/img/pic8-light1.png)

![Different light levels](assets/img/pic9-light2.png)

![Different light levels](assets/img/pic10-light3.png)

The code was originally modified from [mBhakta95'swork](https://github.com/mBhakta95/Virtual-Reality). This little script is the whole reason you can adjust light levels in the application.

```
<script>
    function fourLevelLight() {
        var light = document.querySelector('#light');
        var current_intensity = light.getAttribute('intensity');
        if (current_intensity == 1)
            light.setAttribute('intensity', .5);
        else if (current_intensity == .5)
            light.setAttribute('intensity', 0);
        else if (current_intensity == 0)
            light.setAttribute('intensity', 2);
        else
            light.setAttribute('intensity', 1);
    }
</script>
```


## Libraries and frameworks used
* Aframe: https://aframe.io/releases/1.0.4/aframe.min.js
* Aframe room component: https://www.npmjs.com/package/aframe-room-component
* Aframe extras: https://www.npmjs.com/package/aframe-extras

## Model and Image Citations
### Void Area (The teleportation area)
1. Ground (Texture): https://cdn.aframe.io/a-painter/images/floor.jpg
2. Sky (Texture): https://wallpaperaccess.com/full/149370.jpg

### Pre-Covid Situation
#### Imported models (and other things)
1. Fox (3D gltf model):  https://raw.githubusercontent.com/KhronosGroup/glTF-Sample-Models/master/2.0/Fox/glTF/Fox.gltf
2. Old rusty car (3D gltf model): https://sketchfab.com/3d-models/old-rusty-car-95baa20ebc5d4d2e869f0b549be838fe
3. Tree 1 (3D gltf model): https://sketchfab.com/3d-models/tree-615fbc82493c49569dab81a7b7e535e5
4. Tree 2 (3D gltf model): https://sketchfab.com/3d-models/giant-low-poly-tree-acfd2b7f80894848b56c2ac8e7e59572
5. Low Poly Old man (3D animated gltf model): https://sketchfab.com/3d-models/lowpoly-old-man-fb847d79fdfa465894f30475c6cfbf05
6. The other man (3D gltf model): https://sketchfab.com/3d-models/man-rigged-19b2316028234cb68c1f0bf7b956a35f
7. House (3D gltf model): https://www.blendswap.com/blend/15930
8. Fighting Girls (3D animated gltf model): https://sketchfab.com/3d-models/kgirls01-d2f946f58a8040ae993cda70c97b302c
9. Grass Texture: [grass(link too long to display, view markdown source)](data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkGBxMTEhUTExMWFhUXGBgZGBgYGB8bGxcYGxogGxsbHRgdHyggGxonHRgYITEiJSkrLi4wGR81ODMuNygtLisBCgoKDg0OGxAQGy0lICUvLS8tLy0tLy0tLS0tLS0tLS01LS0tLS0tLS0vLS0tLS0tLS0tLS0tLS0tLS0tLS0tLf/AABEIAOEA4QMBIgACEQEDEQH/xAAZAAADAQEBAAAAAAAAAAAAAAACAwQBAAX/xABEEAEAAQMDAwIEAwUGBAQFBQABEQIhMQASQQNRYSJxBDKBkUJSoROxwdHwYnKCkrLhFDOi8XPC0uIFFVOToyNDg7PD/8QAGAEBAQEBAQAAAAAAAAAAAAAAAQACAwb/xAAtEQACAgICAgECAwkBAAAAAAAAAREhAjFBURJh8HGBMpHhEyJCUqGxwdHxA//aAAwDAQACEQMRAD8A8IpeIpbSyNjlWAmxbx20f7IpV9K3km4+W8P2yad0+niM4mOSLN7PZ8Ph1TSTLVARdAGwAEHsY5Di3mPM4TZI9DYoNmNq4SbJ/LXVV+g9t1oPlvg4sE86KPVtzBMOftEnPtNskJpqahjtfj6TBeJO2NX1JhfsmoCctmGC16lJiyZe5oquhSlNopbbaQvLY953TMfv0HS6e2Zp9MKkKy3g8Z/TRV9KruMi97fVOJ/jMyRNiqqjc7blobBmDxF/qU/a6j4elmGn1Qvqkptd3GOLM4t21PTS18QFIBabc+L/AMc8F0uqDs4lviaTzL3nzONTvQDHpU02Eqe4YLL83Nz6e0anr6FNexIKSLUwdz6z3O/tp1fTN0Is3yhSl0tf5ryd/Z0TRYIBGaSLRVI4s/NNovqmCdCupRSGZW0Tj813JzpL0WpcxilwgYxEkbcaKvpNW12bW2TFiA4glxwd76zrdOzaMWT0yAx6rREEeW+lEhv7OksBaRqnu83tENxk+s6R07Y2z4vJFrZLzj2xoumbXbSXtDFlu8F/bBLGh6K3cVDiLEzcmxcCW2oQumUl1m/Fu8/4nEe/bR9KZZuXgkkviHmJZvpZQcxTwkoHakn7eLe2hoppAnBiCWczbzd9pMaokENrpWtuYm7GZJOyEH074zp9Pbtt8rZue98Y5xnvGi6tY0039Raljbh92J9Rm0Og6VIBdqff6EeJlY/TQWg6hTzIwQ57RM6zoJMIvJtJsoJzedH8OseolIC3b9xMWjU1JtZZVqSDvyefSL3vHbUuhkt+O6WaexThmJukxc8/x1pS15fS03Knvk7+M283dIJPm9rrVtXCx/ez3fM6PqT+E9U1LwJDEsEMRb37To8WkYM6nS3MXKpqqQiV++eTJe2NHTXIXAJWSd2JxaJcGPsa56ZVSiwx+W9NRtZlD8x4jDGlV7o2qwhdw+bc3x9eDRs3SGI3EkIEmFIcRfvjjw6LqdZqapAizHBT2jmw+7zpmxaVPxNKoNkqUh9/fMaj2bJEq2rDuw8hZvYfNsM6VDBop6Nm1gAuYpTuz5/d4d6xTSG70tShDAlyxFi6gWnSevU/LS5Jgm04RtHL9fppfXqGd0ztkeYxM9s2jt2nRBCP2FX5X767R/8AB9P8tP2q1ut+XyP1IdX1NrAzupmZiKoQMcxGe57M/wCJ2KqFxpJz5Ob+3HGp6KJhZcB6Z4PsQ5M/TXdUJLyloIsoGQ3cep7cOjxRD+pRvpiYLVQkXPp2f38GkdMQpIuJfFns3T/dLW0z4brVCU0yjN3ATZDtZZ7++spoh3PyrO2FiPOMyfV8aNUaaUBfC0tF1ZKN1+4t/pA/fTGu5G43F+zace8H10dKzNryEM94n+zuRnjxpTS3CSmLqfMzaVWbF/wCpJky50a9OaRqRmzyxI+2SlgOO19F1aiDZO4W3Je97FvcYjR0V0z4ZSJvGYOLcrrvihasz4ZZUgLHiCe3nRNl7A6nRYDdt7SSl+/6cW0PX+IWU4va7LDfHbjTaerTUTnstrWvziDMQj31Lv2lMPpi6dwJly3mx31Kx2Nopqrm5OS+IsSzGRr4iI5nSaq/wwNUPCT5w2+VtjVVIU2tul7RiwufH1PGkUrVJ2bERAfWe39RpTIbTRA1UiLG1MANqbWiZ+j9o/iK5ndXaV59yX8qfucauq6hS2ZJgIyR+lVrnbuak/atXeFdqMQlhY4ndbiT2049kYUSt+zDyzbnHc5n30qropudshuDuJiSeyW8PbTfh/iwilqiptiXiQ8To+qVtYEwmbXS7J3gm8a0m1RQJqcXKs5ZqIizfsH79FX0p5n6wrbHf9c+J03r9HbUV0zLeEsvvP9d9AdKZXBu5xJaWbxHjD31JyTUMCmLSkpARMWjBxDH8tU9WkYrHJu/vSEZ8Jn241L8P8PUnNNTiIw2XkncdvvqxpiGzVMyeIUU/rPnRlCYPQh6JRNUNORqpLrfsF5i/Ojp6rSkBspm5TMU8gp32stsq646g0UzN28R+XB9CLTfTXoNfpQiAbe/qhwG6p+3Fi8v5gAp6t5X5hJVS3IN/4Hk1nRlWWHK8x9LTfGlNMJNXpFclhZjDNgtEY76Lo0pLDBfhxc3cxdtER3U1PFbNUP3ev0l1x/ZcFsglu/jmbo0qjUG1gRyXsWl32Ulj1Ve+i6PWpIG0DDdsWv8Acz5xN10VO64G69P9lzHt6fa2TUsYkGOqrEAiGbeb3m82jvn7K7rDEM5n2MgF8cGhqWlpimVi145tNpM0zfH01vxFSVGYaouGPtPAfXTBIV+36v5j/Ma7XftKf/q0/wBf4ddrX2/oJVRXuNzbu4mZm3DO73/dL1Omny02ULCfM5Kp8PjzfTfh6lEC2JPZZnhuRzeLaTT0GGnba22Q/j7lzsTkNGNMCjpdSN0QcUx+IVnKMM++bmt6m+mogCCWlxJiLsZlQ0PToWw3WYC9gY8F+0W40VbslV4iLxPdw22sdvawMjOqwyzFxdpZtVNsy1BJyva2fD0otQO1Jpqbc8pEwrN3uYDTjqTQUixaTuB3bHpqLR3xBqfp+kQIZWJVVpIkJvu24gi9o0LUAw+jSG24P5kk2rkeJqt2u+NG1HppE9TA9o/cWv7Z0PQ5gKYYPTPnBgjPv9z/APhbTtb5qQX8fe3Btt9J0PTZpLsHo7iqndHMsYdyFr5EvbCzE6Pq0U1IAgAqWqVvjm8zKQTpdPVG9XBtJPJYZZmLc27M6LqN4vuggxCESd7Q3P4TckSUdbegsMsPirB5Qv2j9KKCGViZIYwYNxPzX82nQ1npKjf7QD2uwfwPtrQRj6XizFg71Mc/W8mludFIXQq/ETNPLaQxm2X9S/Gl9aoS268oTa16ZQzB5y+DTenQG4ajLaFIqIHsk5nB2DSeqwpTubZpUJsc/Qhz+4SsIEdelmlplqgnLirNrNp5tHadUvX3U1CYuXiUu47RieO06kqqi21GSCM4ta0YYnvp0YW3aPN07yx2/dbbVIvKB1dFVVNNNbmYfBEZxznwaPpzG3F7qS4bTiYMf+7U1XXL3mmO3ieZDOPb30z4UqKTc1W+o8xbFzLNm86z4uBnkaTNsfMYhFMWkvGIZ8646qxRAbSAuxSkymZhjvbPGi6dCyCO6nbKfhw45dv3/WaiipmJ3zdastreZq+l+J0JJmX0P6NkabQLcvM3Z+p+/wBjmlGqbnZ7N5gfE9/rqK9JtpZvB4iLgwSX4tBnVHw/VUY9X94THiIafm+jPZ0vGLKIE9VZ3FG55qaqipLAk0w2M/pzps2d1UQNJUgL3sDFrncHxplHSpe4hMmSpInCTdPOlFO4/wD1HEW5vLGJZKUDxzc0+SgCino9OGPlncpTN4AKZvNp4L/dfWaC1N6S8tlgtiWDtyM+Hvh+oqUvAt/KkyEW9ojWlEVIUnembs4xMkYElPto07GBHxJMVbjEw24H2SIJ9tB1Y2wws8ZHxezEW8MTfVnUK4t89Mx5LMTEZpOP10j4n4VuoiSQROZlS6499SYSSz0vyf8AV/trtHuo7v8A+P8AnrdaEXRXFTTVcQ5iZCzGGODF8WNWVdSaVpBgEpJapIh8uf11J0OlVVO4JZCO8h9fze2qen1mlhCq7MHbnPYJ/wC8GSFewaOl+0pmphsimeZw9/363p01TaYQvCmL+ZIjTKerUVpTMMzP4SeI4tVfn6xrelRMYbvOL/LN/sj+s6zMC0uDaGoc+m76nDm0Mxi/7raZRS7vSfLG279vOOZjxwFHXkvSTSo5sTNoS4nMsd4lm6vxMqFPqck4tM9y9QfXGpJsKGnVIhpYRYS1NpvxNgfYedM2VRFNyEZYi/blIp/qIn+OILUizN2WGIESXtfxzGmdOqtKW8gzweELg4PqdrTVSgZgeGCOYmb2bTzaOdM60HT3bdzMyREpDBHcpsXzDe81RukaeDBjD9Jhfv4dUUdTa3pZhjd5AI7Pdnu83WSFdWpyTle57H2eeJxhPTolmAa1ik95WR5LYtIRxq3qMTL8obRi0QiQw97cr40nqURt9LF4tKI4xi/66VkOwKK7LSgG2Zlpiw0wcZO6mk7jLUjDILmVI7vzH0vKaedRQKhiAXfPPpnOFz98aXQ1JV6VuzNKz53ZuO2HD9dKoCj4bo01DEMDbckP09ot383T0qBgFgYjEePaZt/HR/D0KzLYYDljgOf4ui6dINopq54QnO6cQEJPOsaNRQHU+HWsfEwnzQ/Lns48edP6HQpKqo+YGpt7g1YtY9yPbQdQ9NhEPe7ZiMtl/wB9b8R1Gi26047kq/4SaHuzi95ttAwaWK4XJYckiuWZ473dMKatpUm0qspYzPnkeb3xc0MvyjLtGZt4CLExH/e76KaZjdY7v4e3nj+ehmUhHW6dNO2rMMWtl8s2Ap7WdNoPTU2MBF1tk7BD5tidZ15KsBMzEWta4EPtN6tTfGPqbTdlMYJ23jtU/wCzqSmh9BbYa4sMwn5sERhgbH+5QUHpj1Ym329ybZn3zpc3WfSREQwUkshbuR403o9UmIMT7Dys/UiPrqcgkL6ozSFKYEqtiwTMrMnDlzfRdSkElfTCE9p9P2I1nUpCpSbER3Jlv37Wb63qVlVKRCnaXbxCQ8zi0xoGeAKqlNykfKfwPMtSSeNT9e9W5pRIm8d7JIQt/e/N6KKqWlUNo2LBe42xgj2+ui+JKgqgmbdl7U7m3b+etqmUEX7Kn81X9f4tbqeK/wAh/wDd12tx7/sah9F/T6qbaQFlIuwBlqiABm7yxOnHQANyNRuu8SRt7lmbRqP4ehmkbeqYR3MGJfdZ7XNWfE9VqaXkJm8eosXxfn9L2xluilQZQpRE7fSQcwwRLEov1n7qqohkWnJGbmIu9pnwcGmdOVQm8BFnawSkT2+waGGRr3FRZM+0RLntzOgtiGEuxUVwQxsGfe1y8I50A+lkgaSGR9oteZQS1nIGm9TrT3qPVZqnbzYSJkPs6Ho/DuFja3mTcYxKSlvP0vtUrCBvT6Em1jvTIl5v6r3iQxxa7oaa4S76S5cxDkyYPr5NHXT6cG4pPrMxEe5f7Y11VUMVYvLKckX45Ps9tZ2JsEywMxKcDE39+e46Ovbt9OZj5T75zEWi17aX0OulXEFsw+1R29/ze09vLlFBN3mcStvPGfJjWYDRr1JiS4WsjNhqQxHeLdwdF1OvALdvTJ4XHeyv+LUXU60bdwbqWmyRZvVOLzP17X07oklm6n0mW/LF+0WtOtPGpKJDekclkCzGYmOMzjmPGt/ZsTxKRFu7jnnHfQ9SrbSG61NrWtTbxE+mo9sX0rqV2uqyLFjDjtlvY0QyZ1FG2qPwyZeHK9rTEZte06p6nSpYq2g7YWJiePsTjCal6akWj05Q47+Pl8+2jr6og423nkJXjDl8mppyQ34emPmlxMNrRFrufVe+MxoviOmMVTStoWWYLDhw1ey441u61iWoFLPqL7R8ThmR0vqUtRM2amQJjtzGcyr6e2jktHdCplpZY+U/Nf02Sbz4JIjlL4eh9OVJEeDlzj8P0+4dOvbQgqU7onk2CFIQnBthZfolQDOGGIVJyhLCts++MmmCH01JBBVUyEx6gs8JFp+hpPxPUpAbs3iUe6Wvfm3IxOg+HBp+YatzeCCHFI324vmXJZ0VXQLMXCqRqYcLj3Ls4nRCTgXRnSoSl9RCWrz6b9peCmLQlrEaPpJbgi4XKp+XHi0940NO4sFzgAA3bpeMCTCsnudTVFMrUZxF4tblX1Y8/VdkgvmikWNq7sRV5zfiL6LpLTUlS3pJwO7beeL7Xveb6L4WDogm30pHGGz5YWO5ONLprYvM1QSxmJz4mb+17OjtGnBR10qprIiqQLcFjHlv7PtpNUXvb03xA0/rftbQ11y1QTVdJRkfmh5uRnv7qurRbMEfWGFm+hY9gjP+E6v5X/N/vrtTbn8v/R/7tdrcP1+X6gP+H6kt6QIqkjif0InH15NH19oemlBqCR/Ml2ck+/DGNOGaWand3i3eXC4b3zzgZ1lCIpG0MnJF88EOFg1mbAR0Op6k2oW/6owYmW/s6LqdBJqaoEXMpexeCViSQ+7pfR9RIi2uJFMW/DePHZ99N6FLelTcA2QsMXtyLwN+OJ0ViKuh6hS3vPtg5mL9tFV03h5I58YzVkzOndMlZNrGDkhOeWQ/xHfU70NoFPygkFkHsTF7Z/NM2DV5cDI2io2lvVWU2so2gHljn30poWKtxZ5UaQG758PZvjRVqBFgqYbvKDE25JzfzdtVf4WS8N829KWIH1WJvU951fQmSbikUZIKnaxubXj6d/fwzcjV2iCHj8s/mku6XT02lAiRVfIwp7jxrqusVI0tW0GnkteIkmEg+hHGtwAPsZIhNxGReEiI4x5h9VLcbSVI24SVzhvbud9K6BQiireIeZdqMG6NtRD+6Zqq+LcFfqtJIRNt0czF08XzofRAQJmMswUpVMXz3yzgzFgq6UORTPuP6E+Jl1nw/Xqncu0Y4hZGe8eqf8vbRft3fAzuL0vkgZPc8wXLXoaGhVPUkXkkSO/jmPp350fw/VeQkVP7Vhm/F5+/fSumrBSQHv8AT6RJfvrf+IXbuIsm7xz3YWmIi3iBaCkf1a21wCrJ2myj9vsaeVqxFzs8xbJey2vdbMWnoqU200nBmmqBYl4w3IiA99O6ZTHqEblUUUxmzxIwUx7edZaojQN0wpTEsGLJKTLYgIbGgp6tOJhiSJlzC4SYxi1R40NfxIM0tatqbR3WEEiOAdB8TRY+aJb4MW8Fj2twZUuycBU0FsbaXyZ5jixPM/TW9Lrysv8AmCEG373E3++kNCxE3uWcfX6W/lGi6VS/i97kK8drhB/DOqCH9OupanaSDtm27M0zmIiw5Yi2sevdpfBLVdvHGMJjIuL67qdPdSMTiRZPTnDHieQe06R12v0xm95vFj6N5j2eLWKTCSuroscBBaHdZ+n4h/TSdwM2L+knHZLPmBmfpotlV0LwDDdYzbGHjt9FvqXcDDOYuTM+LjyXe06ERR8RXBTtpp5csxMzE+XM/Mx5n69CRIh25ac4nsn2Yxp3S60LRBfPJVNUrJz7cus+IhKhlqq3eV4UQvlfqfWVUMidh2p/y/767StlXev7f+3W619zI2n4iAjcwGKZbSxyraxzBbT+uS2qmxyx7z7Tz21FyTV5kdtjjMsXv9ONXV1AjZ5WYkZm8TiT640ZVEbEE6lVDSREs+W0eq+eO3fiM6lEN6r3c2V9ucPZvOtreIkCpu8CVY7/AKMTNo1J0n01tRS1RaSeRVIe3E86FdiNo68BW5lnB+G4p4cl/wB2t6QbmniHsRcgi8zJ9nvpHRGd24d0Le6vNpJkC3jtqk6p4fVPHI+mwOE9186ckuBoOusqX008eC0bvZL83fa8sXn5aqi/EQ4vhj2jxoepK26l54w3n7qDft76ynqu0eRxb1K2AjjE+NKx4QbLetWbZqOapsMYcpJEz3vi2omm9NU+mbzfiRLf1Hk0+pmeaPwzyW2x+t/Eamo6dW7beZ3DxSe7BFhHOrBQDH9OncQ1Itp4CASZNpA9srEYL4guTSkRSekyN7378TlyQaCikYi7wLi/iG9ofPjQVdOCNiU7gKYfo4cm36h9VbIa9Kr0iixltdM/VlxJAd5TR062tZixYVgGLn3Z8W11G30l6bPEe4OHv+undWoupUAfSq9kbrP7vcNUsRXWtSp7ZkjJixn2t5s/r0TSQM7apSPme8GXKls6HoUgFie4MYv/ALdo0rq9KKimmVIzNv69Pa/00bA3o1NTJU1VIt8JgNvMzOfwmmtDAki1IDTMlQ/MOci2/hpXT3I2brE2uzZ+hgzDo2ufm2wkSCOPmS35WmY4O06XsmKNvqQ9UZR8Tf22dpQ7Wb1ehVaqRviS8TDHt/voemVIUuCNxMhgk5DB4ajvd/7VqpaYw2ZLsZmLhEe/tqybRpQKy2kLLeEL28vE4s+dIpJUWds2qiG8Rf79sau6Emb1YswZO/M2+mt3bWCnN4l/L6oTGLGOPYWUAZT06tvbsEot548rd7kk239pS01YhYJm0KF07wRf+XPxFMQzU7typm7AGPTc+gvgaenFsq3MJtvE+84XDrDt2Zbs4CkgLhVLaxBFV/G4iGF0dJFTvkiJ25Yylu+nOdwlAGeDtfsfWY7xpVJNcrDSGLh+Iu5YtJ+7VMivZ3Vql2jDfFWYJcXCz7/TSyqqpV5Q4mzITmfVa2cTpnxFWwXbBNl7Nu5nvj92paKV5ip+8QNmIUNxL3+7joR2+jv/ANX/ALtdqf8A4Z/N/q12mEEFHT+FW9S0nNJZskf3vlx41nW+HelQFUyt5ieA7pAdvwut+H6jTZ+aBIqnJkpi1ke+eJ13xHSGBrQUiJndTVbM3nEs3TzquYY2J3LBIriOLTyyN7TwU84X1KHtxVwXvAje1zvMzbmqjpAqSMTxxDUR+vJ57r+IqmWmRZEkmBlcYGl+530ypoJAp9ZgarWW94i/fcJFsun9VpqhmcmIJuZPrH0TWfM7lwxBfbiIKssfXzxpT01qYJbgzZNxuu/iZ+4EamhkT0+vmYkW3G2UpwTyX7rFtG0FjJTYlsjyp7L2jgxruj0KkUjcS9ixOJ5QPo6d1YpBlpLzSTKJ2yM3+98aXugkCqimXlE473HNm0HiNIa2puHeVvNhPdT9NU00sNLZt5/EEYRlC94z21vXnbPZhDlzl7x27FjAikX+wNsVK8Icdu9157aW0MbqvZ5O8n8b3nTHoP2Jki2JLff6mj+H6StpxGX2C/l+ZnExJqn2Qhd0xhJxF8Xfo2/no1Q4/he9+/L4+l+6vSgdhNK3sTZsk3/Xt5nd0BthkUtMvPZmZynPvqJmUVP5SRgle0N/M48ydtM6vTmndTwVD9G3MTM/rpLU7kM8bW8Zt2szx/Bq+G6ilpX+0LjsFkifcYtzZKLLgmqpT5ATkVVhkgxNm3aPqXUQrXdueSOBnAvY7rFXtqvp0CReIkTIpE9lultSnQpu1IXN3mRaQm0yVffV5IhfxHV24q3QtgtL6vlwQWwfTVPw1W8KYNtkJzeJO+TN7xpVPTADhhqIzEghBDj7fculSnHh7IMgP0/T2NGUQKYVVVVK74VQFHHF2blr86d8OLC0sEyD+abva0yd2mO+hr6nri0M4wyxM4ltiL6KNoXiBU89k/LEeDxrDsieutKipqsFiM8pHe5V9X6MprincXv7+rEAMTtmzfHjQ9f4larTg3GG9rXspuu9wvoqqApi7hiq22SfMpt7w8a3wDH9LqtMyWHGVPbmF/da+l12ubSpvPKP8G+ffzoaq4pWCYBkd224WPNuMLbg6uhuKmuIqiBvtvlMMLDaScmsxFsYk7qS0pyWJtN7yBZ+nOpCmxdY+hOPU3lLduOJ1ZRmuC1TUfW2JtCKW5O+VVkVRtlhRIvJmOJh+3ONKqidEv8A8p6/d+7/AC12qv2HU/N/+V12t+b7QSw+t06SmVnay95Mz/tkjWq1Fo8RaMxTFx4/Ttc+vQibaDjbH4otO20cxzjWiVANWCbfNiMZn2ONcpodUB1K7FMXibFqcjeL3i/jxpfxPxEFtpVPNIRzFr+JHnXdO1SOVqgtb1dnJEX86L9lSQM1GN0Tu4vDl0wlsGuRRUnqY9JiYnJFXKXQvJbxp/wvXKhkpDkM1SsDLaX24+k/R6ZS7i+c2wKbZz6rTHObaZXRU34kEZTbtPtkZ5Z1pwwGfE9aqr07SxMUgc/fMXmzR30BQwyElRhwKBV4JRfaZ1vW6hAy+lntJlYuQ8GPNp0VdIUiciRGRFt4sdh0TCFqBPX+IqpCNt3hnPHlZH799O+GomaspTO77wUx8zi3nSup06YSlqZvFomqpiGZ5TxImh+MSh5lhieLs2O0Qf2fGrdIjdvrJwh7Ym31jnt762noBQTGIQuxI/YQYC1vfWtNoPlaSaktVVkzdx+7TqKqZ8NzN+4HHeV+mhtgkZXXTFVJuMv/AFNmMt49o86m+Hver0955nCcrb+p1T8VSr83nm6gAfQAmMaRvZRH0lqj8XE5e1/b31LRuZOKKN25n8KMXIsn8vbmNOE21SnAcr3b4iG1/wBbg9Qqe8VDebRmO92PFSe2lfFUxVBTMLL3ABt7Ex7z5d0zIT071pG1kk7uMGYHCfrp4RtaW/m31z8pfOlybmowRHKATfGS36x3b0euT9Bk4Hzb3ONDkEif4zpzsClNqWiYabFssJBPj31HT1hntXSS49Ui1Wccd728ej1KAZNzBALMheFb/Wf5aXT0bISMLBCxxDBFo7p9NaxySQpg004ZwbpsisqZkgniLeda1Eovkq4HEzYJ82JM6C8TDywxfvPIQdvpnTaoEWovaL3OLGB48RPiHaG10z3ePS5jIQY2hc7ukHTtkCnDLTug2l1wTVP0fd3T6FVJ6qVbykswcWLcX7WxoWCn8ec3ZDMmY8HvE6yqKBfxPSnp7YH8M1Enl5WST+On/EdVaNt5bHLNmXv3j9R0ilqKtraeGIJ+t7oRAsaZUUMxO7mZFYmx7zHtnusmxXxHUQMRN2EsN4hBtebfTTgVWLU7VTxfi120FoX6TlUIbZlyhDe8x5qeZuzPNPT4VZXzmbN8f7ZZ1ZUZJd9ff/T/AOjXar/Zf1JrdU49IfEHqyDPsHZ4GM37X9tLpqhuNPrS3cBljBHD24vrfhulurrEmEqKVtGSWWWctiMGTTOpFTt7KeUhslraKTg14od0+gDZipVg7FozmY7RnUYWJUB8eplqxCpbLk40xrwlW1JvzIyKR25/fpdNY1QSRgmIxw+POOMakmDGUfKm09V5Hv5+hmS17Fi+J/K1KMSQSLmLqfQtLpdPVZntUk8bQJIiSce8Z03qVyXD09zL3jFSn1/TRaYcG0Uu0Kbt1J8YxiYJ86nmWWcpTeFhS32TzGi6XU4KpJ2xmAi3N4q4jjWfFdJiUEl27efpnK8/wiWx2Z8PSUzYQzm9oxg9M2GM6Z14iZS/YskZzjHOWL6zewBlCeBqsyhgnkiHCaCvoyCtXzSluzGS3LgcOcvNloz4ahFQYb0VNiJtKWYlm7EScGt6FIbcEZUk2t7OCarf0aCl2iBF2C6rVSAJe+6C0EZiJ0zo84L29Ml5cTYtf/eHTBBT8tInqWHMRYzjF/3uhaZArJUhtHL73j9zGmf/AAtp2rOam7+O9/Y2weM6TXXupVWY2jCJcwy3dtnNubOjmDTSG/DiEkMu0nE3882Zibc20v4nq0AWnmJuJ7J3vczo+rU1OYknvYvhiRPtP3GrpxDBIJlRw3e3BMfI3tcW7B0D0qIofV6EtUSwXkKeGYHGDtdnRi0jYiKYvOJgxFv5wOgKapjkuWtt3bhmRgBJ/tGsts9Rw2OTEbWZn1F/0nWtkgj1gElO19XarH3m34u0a2GlqGflDFyvbmcM7Yxk7aZ8NVHSBshHgsgIWW0wGbxiVUV2LI1QTlxOS/NuM6OWjTgkWWncSxCxdu7TaYuxc8dpPpJHyQwwuYZbszShSfSozbW9ailr3Huk2r/CksTcfocZ1lBTAVXKm62mxI28BmMd9bMhdTrFhdq7YWfWXwrMkcfbEh02Eq6ky2ysQI5e8+LkXvo+t1OZsxTIphL55mIfuazp03KSbWZvxHMSXZkvK9tS0CM+J6U1izfncomNuZEm/ZnVDSVT6kZmqbmfsfNGMOuECI2wyMXpJOBhpmHk++l0UKVFiqGJO9NkIzm98ay2MJHdEQuwjHDCwJOQs2j95oq6ZaslLDHFQZ5zP8OdbR1PVZn0ttsxETxmSyMyY411LNUXmbzOQ4XFvVb6RN6wRT+26n5X/Of+rXan/wCGp7H66zRC+f8ATUs3phTcNw1KxdqfPkk8WNBmzepJZLxEWVvgxc1vw3xHpGmzJTclTi+YnxyfUa+oVMTEzOOeWbmKe2XTcmR7QNItVVo25yLw3ZkcOI5JT0aW7WVFQxM5GYIugXhseqCLGj+GqttasxJ+bMy38Ef2eTXVdNITPdhglSoV2pN4H/c9EzB7bY7ZpYvT/OP1DRUrW1BBSVHrCzGSnlA5+zrel09rUUqtoJuHmZiwAnC5jW/BqVLzVbFgCx+6+CfpqqGzShHdai4UwVbmr+6xExDJYte6e2i6vVuOYJLnp9ScoW0krbpPqZpE8W/Tdz2zbTCmtDbuQiYczJVEBFQ0n1fFiNSSYn4jyqU1LiIMyZve/hXTKOp6kmn0848zJh4niXvcSopMuRHsPk/nh0fT6/puLEy7ql2zO618xdmzpiigZRS7vSfLG2+fEc/WYe3CDqkQjCTcgptN+FsT7DzoOv1e1F6r5kgvMzOagzz7az40gtSVMzdljgRJe1+xzGlYgyjbVEUykIq4uOOUin6vtpRbhAjxLmDE+0YqedbRVXFLeQZ4OwhiflH38WUsuL2RDDNNWPOe1n30JAM/Yvp9MhBfN7z3EzHZni7Oi1Szu4IqH1E+lvNonn6PKf2X4amqCPTaWlGPeGPtbAL6OpUUhBINmk/DYVVl4ONTNGTBUjRN4tAyTdG8zYt3voHrQ7XD+ZvmIZvFvOJm8azqNVqjbttVYzLT37jxPnWmKbHOwIC2GWRv9JM4mBsZV0XvFj0xNVpifqL/AFZG8GZpmeI+mLnNpj+FNIptKmEHMZjjnj7c6V1+ne5VUbhPT7ykSxeMGNGL7AP4upqCkjlg+Y/dDM9+dTdLp2atu2JFi5F5M27h21cUem0UhdtJfntMs/V+stHTl3VX7XjlCe/0xP2k6HYnp9PdJUbb/KxgWJkiSYfYzp/S6PpPTM7vChDLMyn70wRrv2d2rkBsY7z9UnNnF3WVdYVJ+SarRcPyyx3jH0La022AXVqHc03kzMsyzT5m5DrKOtFMt5pYT7JGF2z+LlLTpfQ6mJoq4LnvaMTiZwnmzegCjVQjBVTtFe6Wdss5/wBtERsQ+sYLyrFtyRFxMqCynPbItVI4AgoYm2LBF3mSeTXdXq0lyqqCX5XtORfzF5JQ99DU7qWpWIg9MtoAYs2vcxN7akuyofuPP+Y/nrdeR/xD+Wr/AC0/+jXa3+yyCWW0VVUgFm8zxNrkef04nRV0iyCRwJcb4Bl/nl0NFUopdiHkkmc9/wB541u4pSlJOGU4wp/C9+xbDQxRS/DrDAw47MT7XgEhufQCqhGWi8ckE2973/FJb7oW9TTSpJYyDtjLmUYzpDS1X/DC8nyu7EwZG/5YvnSsSmCiuY3G7aM3Zsql7iQ2h5ZnGipaGk3G4xaUEzLm0Fo0lSqiAJDCssH32guf+29DbTSTuy2mWQt7vH6d9TVAH1SJT1WUBtn98j+/zo+l66dsJMXVM927M0zxk7aXX0YqITm8h/OSHR1dNs0od1ZHzEQR3vx4E4JGVdCApmaobWLFh8LFXH1iDS+n0YHvKje/ZMEp27d9UmKdsVCBC2Im8ZLRe+ONA9GmqmnLebmEIn3z3+XzOry7EyqghHmZZ9MBP0JH22vbS+p0zZ6ki6SQyMMSyswcd763pUszzKkTHn0572xbu6f1qKajI0kxPEvbzPH3dScFsT035EqzwPFLfF+x/Q6YlMixLGL3/qP6yrp1NNRLZv6RiS3JeIm2d2Y1lXw82sDNoYKQhJC0keMRnS1ZBnw+KpRGAlAPJHy2+j24Hp0sxVYuRZk5ZjJSERhzNtH1epKbqok/7Q39k/TswpjMyjT2iOc3nJPD5jWZZQZ8X0NxeGOTDdc9vw/V8mk9B9W1ta2FBvkfc5v2nW1rVS7YKVD2nKDzG63fvrug8VNNV6Y5gqUfVee14j9NK0BtFS+q9qsB6r2DF+f099P6laTutEB9cSuLJ/VhHRr3Mi1MDIk3i9rBf9HGi+F6e9q3S7apKZvYLqxdIsYZnU1yzSU7B6KSWaVqqIRlS8E3iFx50HW6d5mbPJuhbBVhGxd51R1K8pw1NTgqtxbKBf3zyjoxuaWYhY7XII5/fbUu0EdD6AjbyiXbNLcILIwmSxzqbrU7V2oR2GYwsiFj1cTC3iqXV9SXsLmMNBe3Cer3htzpT02mrctW4qfltbdaKmfM4kn62OwkLrUtQRIYXmc03i8Zw499ACr4pXdEjE47ywy9zGj6vUuzmG5Njki8WKUHir751bQKRUxZ3VS8e319jhVJJNiGNxvyJcG4llsXTa8376d0JbOJiRhpe/nv2z76L4roPTmKs4i4MFoWMSn19zulR6YwyJAJKMnEXMyH31qU1KFGf/KOt+Sv7U/z12mbTvR/91/lrNH73ooQHxc2OYCphtLaIHyXjjMaV0oUqp8WwAXLP9lFmW/nQ9VtIRVMwJhYgW1orY4i+ipWqoknilTGIzMyznz4hiEBvTqpTbTA1ZIq4eG9sH00vfTerkqcOLtoWcM5v7GmdRZgl7zckBNrewvD+FvOhqrppZ2yfLKcAcEzFrzaOMaURT0ZpKXMKMtpxD7z4XQ0k4mM7fPzRPPH0+hrKa0he1l7sA89i/19x6sANJiI4vEHvaqfZfGsbNSNop755IMRFjDhbM5LW06s6juFsvfaMHF824/LfnUO6apiYtSgyvJZILGdOgar45O1JKE8C44+1xoAK64JKplZxIX+kScS++irfmo7I+zBcO1st5/SXq0fhmCoqHd7zCxG3mP00/oTESK8n3/eJKczrTSiSHdDqG3c5uXvZWkfEr+ttYlSMWSCI4GOOYw2GZjQ19SaVIizbOCfDaG3Z50w6tibzEIxNP4vFl4cQ3jWPZMT8PWUFRTUw/SGQ/zxF5bHMaKpvJa5ZFjmJ/g9vDpXU6TSoQNWF7IJzLF3xPnWdTrDEbrPzXC4Sy9kniFjW4mwKDpxDYCJvxUGVk5PGTtGbGE2hci5DS3pxhifvpPRaF5QWJmOyYLzVS8zL7jqPiqikN1RUDBPtJFJG4k79raGhobT1R4ut0JnDYyzEXCyltDUEgN3ilRRGwcsKzL9tT/talmpgGJs8kNjEbfPqYTTOv1UaaqWqGcg01U87rTkw8376vGHRUNGmWMcJCRk2wxP8SMaU1NEtM39VVTYXk7wE/bzZfXo3TTYfE83t2Hm78ukUVfiJt+JSC+YvZW3aeNPjRT0UU9SVqklZcybvBYbHeZWOV1PVwQZ3XOEbHgLRh0rptIO5sXlkIflaYtPq8J9ox6kVJExH4gmSMczIHkh5kakkM6PUiVZBJP7Pcv4GOz76crtakmM3EfVeeeP+rHdQqi0m23FLUm3JJ/aXP040fVqpLeoYi0exFh/FMY8zoaE5ikpGyO43cRC1VJa2YeJvfQ07aoqp4GFMe2Qn+XnWdLq72Bdoz4zdMIQDZx7zpPR6sdRITzVLBx6bmfrpjfYMd1a4JqGkAsgS3Fzae8ZJ5ZQVXWbjewd5Ns/NFIT50967HqnDDjmOGG0/p2nSd7Eg+ZYpac3ZJzxe/tqXsBX7Wr/AOm/enXau/4uv+z9/wDbXapfRQS0RZliuYVnde7MZltFrPfTagqCkmZjiY7jiQmxqSqpwcokN7ZA7se/0039o0dRqqmacnBUvPiR7X1p4z9RMo620qpYiG12UtbMC6F6slMtVVMlpmU/DLdzEzcbRGirr3JC1JU/NHN4Ic2PpxplXShAKTBINrKyvg9vvqTS+pJmdemoPS1TzYvb9MFuPpbKdvpuLeJlSrs8ntjOldCuqrqNOI8mPb6T/U6r63wwVUpIt72xHv4NDrYxUiP2++qktfeDETEsl7sMxm53dLKpaB3GRe8HK+af4aZ0fTJIlVMSAFLHERaICMyZ0fUBpp7pVNjKckczjzJiy4ToymJ3ZJZzCisPE2wYz9NVVtMZlhQk3NMQWq9sZu8wahppX1PNMbg9RFiKXFN44fZXW2KVFQGKsWn5pYTJP6eWERX0OruxEs3ncLEYMEk/RlA0vqUyygMsRtILxVxJab+HOp6qio+ZMmMHtL3qP8X2MrAqKmL7p7pwWBbWk5zjRF0Oy6mv0Vc/KxIzTCF3jLL2p1DWSbqaphOFk3QkP9WibRp9HUm+CDcLiqPUdlamc+SdTPTvkSuxe0+Jt4TmbaMVDsmPKs3e1PemG0ql7zi8kToviaAp2xNNO7tUd6WKiLbZvezfWFEF5zDe3hgzzbXfs/mNqHPaotLm0RBjPa+lRIGLcNyslkuQ9ubcWYl5s6mmkKqW2IRbMQZPliD/AC6DpdMjm3KsBcT6d/73jTunVTXZsliZmmqI8Tzk76MmaRP1OqXLEvDPMQZhx9r5dL6lIUoFLykRzxB3/qNM61VNgWpjm2MQWec+PZ1vSrv6RY5mIcYOPfzPEqXQRJMVUrJUoxIjYtjhLVSRNj30W66LUQTUmQ4hmMhBH6kas6/RKrU+mEqXbDwBGWyj/vpXxHRqNvdpttki9x8C/rqWUgdTQwRSotpvtyQvctGIn7D8QXRWqmajBI+/P4XjnRO4cBIkVEyzfBAHchx30FdkQSD1ROHkzPy02e8d9S2QY3tiB2sn3zBl/jh0x6e13DBVTIraYuDxe3saH4elF3f2pS+bjYhZnzjvo+sNIzNiYiXwxGbYvjm7ob4GoNKpPVDeJkOx7tzn+Gs/4eH1VUzKkVRDKB4sFuYe2u61A7SCYnDEjEbvtTLDddD16Wu0FRNUTe3P8P8Ap+mUZblgftKfyH+T/fXaVP8AYf6//j12unihofVh9/5az4v/AJ1f93+Gu12uS3+ZEz+H/F/pNX/g/wAVOs12tZ8EQ1f8yr/xqv36u6mT/D/DWa7V/wCm0aR3R/8A3v7tP+rU9fH9d9drtZW384MsWfJ/i/8AI6n6/wDy6P8AxKv467Xa7Y/5/wBiel8Xh9qv9bqf4vB/d/8AP09drtc8eDJPX8vV9j92q/hvn+uu12nPXz0LM+H/AOZT9f8AVovh8U/+If6DXa7RlomZzV9P9OqPiP8Ayv8Ap12u1ZbHgR0fmq9v/NTqH43FH97/APzq12u10w/EK2j1+pj7/wCs0jq/L/gp/fTrtdrjic2U/Gf8w/rnUvR/5X+I/wBRrtdqx/CvsS0W0c+1P/8AWal+I+V/8L+Ot12r+JGsuAen8/S+v7zXp/CYr/vU/wCs12u1Z6+dgtHn67Xa7SR//9k=)
10. Sky (Texture): https://upload.wikimedia.org/wikipedia/commons/d/d7/Sky.jpg
#### Self made models
1. Portal sphere

### Post-Covid (Present) Situation
#### Imported models (and other things)
1. Floor (Texture): https://evankofloors.com/wp-content/uploads/2020/02/Hardwood-Floor-1.png
2. Ceiling (Texture): https://www.familyhandyman.com/wp-content/uploads/2018/11/Knock-Down-1024x1024.jpg
3. Book Shelf (3D gltf model): https://sketchfab.com/3d-models/simple-book-shelf-free-agustin-honnun-51d928b33e5549898cc86cbdaf966d83
4. Toilet Paper (3D gltf model): https://sketchfab.com/3d-models/simple-toilet-paper-20-448e57880fa744e19e18604e42d64cf3
5. Toilet Paper Stack (3D gltf model): https://sketchfab.com/3d-models/papel-higienico-6990b187d1494ffab99b7ee960ea7741
6. ~~Stylish Chair (3D gltf model): https://sketchfab.com/3d-models/corvus-mid-century-modern-accent-chair-1fded5bd02c94164abc39c98640050d6~~ (was glitchy)
Blue Wooden Chair (3D gltf model):  https://sketchfab.com/3d-models/wooden-chair-low-poly-f899f1d606094afdb75bd5255d5a5194
7. Sofa (3D gltf model): https://sketchfab.com/3d-models/sofa-b620f9934bf34b3193941418b99eb40e
8. Duck (3D gltf model): https://raw.githubusercontent.com/KhronosGroup/glTF-Sample-Models/master/2.0/Duck/glTF/Duck.gltf
9. Bed (3D gltf model): https://sketchfab.com/3d-models/bed-352f853f03194e9dac551e2c8afe7d1a
10. Duck's sound (audio): https://opengameart.org/content/realization by Jason Dagenet

#### Self Made models
1. Cup (3D gltf model)
2. Die (3D gltf model)
3. Table (3D gltf model)
4. Darth Rishabh table decoration (3D gltf model)
5. Wall decoration (3D gltf model)
6. Portal Sphere

## Code references
* Aframe's excellent documentation: https://aframe.io/docs/1.0.0/introduction/
* For the controllable lighting and door opening module (I modified the code): https://github.com/mBhakta95/Virtual-Reality
* Used a modified version of ocean-plane.js. For simulating water https://stackoverflow.com/questions/52837505/using-watershader-js-shader-in-aframe

---
title: Add Cylinder
description: Demonstrates how to construct a cylinder using a center-point, height and axis.
authors: ['steve_baer']
sdk: ['RhinoCommon']
languages: ['C#', 'Python', 'VB']
platforms: ['Windows', 'Mac']
categories: ['Adding Objects']
origin: http://wiki.mcneel.com/developer/rhinocommonsamples/addcylinder
order: 1
keywords: ['add', 'cylinder', 'rhino']
layout: code-sample-rhinocommon
---

```cs
partial class Examples
{
  public static Rhino.Commands.Result AddCylinder(Rhino.RhinoDoc doc)
  {
    Rhino.Geometry.Point3d center_point = new Rhino.Geometry.Point3d(0, 0, 0);
    Rhino.Geometry.Point3d height_point = new Rhino.Geometry.Point3d(0, 0, 10);
    Rhino.Geometry.Vector3d zaxis = height_point - center_point;
    Rhino.Geometry.Plane plane = new Rhino.Geometry.Plane(center_point, zaxis);
    const double radius = 5;
    Rhino.Geometry.Circle circle = new Rhino.Geometry.Circle(plane, radius);
    Rhino.Geometry.Cylinder cylinder = new Rhino.Geometry.Cylinder(circle, zaxis.Length);
    Rhino.Geometry.Brep brep = cylinder.ToBrep(true, true);
    if (brep != null)
    {
      doc.Objects.AddBrep(brep);
      doc.Views.Redraw();
    }
    return Rhino.Commands.Result.Success;
  }
}
```
{: #cs .tab-pane .fade .in .active}


```vbnet
Partial Friend Class Examples
  Public Shared Function AddCylinder(ByVal doc As Rhino.RhinoDoc) As Rhino.Commands.Result
	Dim center_point As New Rhino.Geometry.Point3d(0, 0, 0)
	Dim height_point As New Rhino.Geometry.Point3d(0, 0, 10)
	Dim zaxis As Rhino.Geometry.Vector3d = height_point - center_point
	Dim plane As New Rhino.Geometry.Plane(center_point, zaxis)
	Const radius As Double = 5
	Dim circle As New Rhino.Geometry.Circle(plane, radius)
	Dim cylinder As New Rhino.Geometry.Cylinder(circle, zaxis.Length)
	Dim brep As Rhino.Geometry.Brep = cylinder.ToBrep(True, True)
	If brep IsNot Nothing Then
	  doc.Objects.AddBrep(brep)
	  doc.Views.Redraw()
	End If
	Return Rhino.Commands.Result.Success
  End Function
End Class
```
{: #vb .tab-pane .fade .in}


```python
import Rhino
import scriptcontext
import System.Guid

def AddCylinder():
    center_point = Rhino.Geometry.Point3d(0, 0, 0)
    height_point = Rhino.Geometry.Point3d(0, 0, 10)
    zaxis = height_point-center_point
    plane = Rhino.Geometry.Plane(center_point, zaxis)
    radius = 5
    circle = Rhino.Geometry.Circle(plane, radius)
    cylinder = Rhino.Geometry.Cylinder(circle, zaxis.Length)
    brep = cylinder.ToBrep(True, True)
    if brep:
        if scriptcontext.doc.Objects.AddBrep(brep)!=System.Guid.Empty:
            scriptcontext.doc.Views.Redraw()
            return Rhino.Commands.Result.Success
    return Rhino.Commands.Result.Failure

if __name__=="__main__":
    AddCylinder()
```
{: #py .tab-pane .fade .in}

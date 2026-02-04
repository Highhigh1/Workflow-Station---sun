<mxfile host="app.diagrams.net" modified="2026-02-04T00:00:00.000Z" agent="Cursor" version="22.1.3">
  <diagram id="urvgbufu" name="User-Role-VG-BU-FU">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1200" pageHeight="800" math="0" shadow="0">
      <root>
        <mxCell id="0"/>
        <mxCell id="1" parent="0"/>

        <!-- Nodes -->
        <mxCell id="user" value="User&#10;(sys_users)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontStyle=1;" vertex="1" parent="1">
          <mxGeometry x="80" y="140" width="220" height="80" as="geometry"/>
        </mxCell>

        <mxCell id="vg" value="Virtual Group&#10;(sys_virtual_groups)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;fontStyle=1;" vertex="1" parent="1">
          <mxGeometry x="410" y="60" width="260" height="80" as="geometry"/>
        </mxCell>

        <mxCell id="role" value="Role&#10;(sys_roles)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontStyle=1;" vertex="1" parent="1">
          <mxGeometry x="780" y="140" width="220" height="80" as="geometry"/>
        </mxCell>

        <mxCell id="bu" value="Business Unit (BU)&#10;(sys_business_units)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;fontStyle=1;" vertex="1" parent="1">
          <mxGeometry x="410" y="260" width="260" height="80" as="geometry"/>
        </mxCell>

        <mxCell id="fu" value="Function Unit&#10;(sys_function_units)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontStyle=1;" vertex="1" parent="1">
          <mxGeometry x="780" y="260" width="220" height="80" as="geometry"/>
        </mxCell>

        <!-- Relationship labels (as small nodes) -->
        <mxCell id="m_user_vg" value="membership&#10;sys_virtual_group_members&#10;(user_id, group_id)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#82b366;" vertex="1" parent="1">
          <mxGeometry x="320" y="140" width="280" height="80" as="geometry"/>
        </mxCell>

        <mxCell id="m_vg_role" value="role binding&#10;sys_virtual_group_roles&#10;(vg_id, role_id)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#d6b656;" vertex="1" parent="1">
          <mxGeometry x="640" y="60" width="300" height="80" as="geometry"/>
        </mxCell>

        <mxCell id="m_user_bu" value="BU membership&#10;sys_user_business_units&#10;(user_id, bu_id)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#9673a6;" vertex="1" parent="1">
          <mxGeometry x="320" y="260" width="280" height="80" as="geometry"/>
        </mxCell>

        <mxCell id="m_fu_access" value="access / publish / visibility&#10;(policy uses roles + BU context)&#10;sys_function_unit_access (optional)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#ffffff;strokeColor=#b85450;" vertex="1" parent="1">
          <mxGeometry x="780" y="370" width="220" height="90" as="geometry"/>
        </mxCell>

        <!-- Edges -->
        <mxCell id="e1" style="endArrow=block;html=1;strokeColor=#82b366;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="user" target="m_user_vg">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="e2" style="endArrow=block;html=1;strokeColor=#82b366;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="m_user_vg" target="vg">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e3" style="endArrow=block;html=1;strokeColor=#d6b656;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="vg" target="m_vg_role">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="e4" style="endArrow=block;html=1;strokeColor=#d6b656;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="m_vg_role" target="role">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e5" style="endArrow=block;html=1;strokeColor=#9673a6;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="user" target="m_user_bu">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="e6" style="endArrow=block;html=1;strokeColor=#9673a6;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="m_user_bu" target="bu">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e7" style="endArrow=block;html=1;strokeColor=#b85450;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="role" target="fu">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="e8" style="endArrow=block;html=1;strokeColor=#b85450;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="bu" target="fu">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>
        <mxCell id="e9" style="endArrow=block;html=1;strokeColor=#b85450;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="fu" target="m_fu_access">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>

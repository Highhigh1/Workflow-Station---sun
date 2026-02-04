<mxfile host="app.diagrams.net" modified="2026-02-04T00:00:00.000Z" agent="Cursor" version="22.1.3">
  <diagram id="perm-hierarchy" name="Permission Hierarchy">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1400" pageHeight="900" math="0" shadow="0">
      <root>
        <mxCell id="0"/>
        <mxCell id="1" parent="0"/>

        <!-- Top: Unified Auth Provider -->
        <mxCell id="auth" value="Unified Auth Provider&#10;Admin Center (8092)&#10;/api/v1/admin/auth/*&#10;- login (Admin Gate)&#10;- public-login (All users)&#10;- refresh / me / validate / logout" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontStyle=1;" vertex="1" parent="1">
          <mxGeometry x="450" y="40" width="520" height="120" as="geometry"/>
        </mxCell>

        <mxCell id="jwt" value="JWT Tokens&#10;accessToken + refreshToken&#10;claims: sub=userId, roles[], permissions[], businessUnitId?, language" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontStyle=1;" vertex="1" parent="1">
          <mxGeometry x="450" y="190" width="520" height="90" as="geometry"/>
        </mxCell>

        <mxCell id="identity" value="Identity Source&#10;projectx.sys_users" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;fontStyle=1;" vertex="1" parent="1">
          <mxGeometry x="80" y="190" width="300" height="70" as="geometry"/>
        </mxCell>

        <mxCell id="roleCatalog" value="Role Catalog&#10;projectx.sys_roles&#10;type: ADMIN / DEVELOPER / BU_BOUNDED / BU_UNBOUNDED" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;fontStyle=1;" vertex="1" parent="1">
          <mxGeometry x="1040" y="190" width="320" height="70" as="geometry"/>
        </mxCell>

        <!-- Role assignment sources -->
        <mxCell id="sources" value="Role Assignment Sources" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;fontStyle=1;" vertex="1" parent="1">
          <mxGeometry x="340" y="310" width="740" height="50" as="geometry"/>
        </mxCell>

        <mxCell id="directRoles" value="Direct User Roles&#10;sys_user_roles(user_id, role_id)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
          <mxGeometry x="80" y="390" width="380" height="70" as="geometry"/>
        </mxCell>

        <mxCell id="vgRoles" value="Virtual Group Roles&#10;sys_virtual_group_roles(vg_id, role_id)&#10;+ sys_virtual_group_members(vg_id, user_id)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
          <mxGeometry x="510" y="390" width="430" height="90" as="geometry"/>
        </mxCell>

        <mxCell id="buRoles" value="Business Unit (BU) Membership &amp; Roles&#10;sys_user_business_units(user_id, bu_id)&#10;sys_user_business_unit_roles(user_id, bu_id, role_id)&#10;(BU_BOUNDED activation context)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
          <mxGeometry x="980" y="390" width="380" height="100" as="geometry"/>
        </mxCell>

        <!-- Effective roles -->
        <mxCell id="effective" value="Effective Roles (merged)&#10;UserRoleService / query aggregation&#10;输出: roleCodes[]" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontStyle=1;" vertex="1" parent="1">
          <mxGeometry x="450" y="520" width="520" height="90" as="geometry"/>
        </mxCell>

        <!-- System gates -->
        <mxCell id="gates" value="System Role Gates (Frontend AuthGuard)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontStyle=1;" vertex="1" parent="1">
          <mxGeometry x="340" y="650" width="740" height="50" as="geometry"/>
        </mxCell>

        <mxCell id="gateAdmin" value="Admin Center UI&#10;Gate roles: SYS_ADMIN or AUDITOR&#10;Fail → /403" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
          <mxGeometry x="80" y="730" width="380" height="90" as="geometry"/>
        </mxCell>

        <mxCell id="gateDev" value="Developer Workstation UI&#10;Gate roles: DEVELOPER or TECH_DIRECTOR&#10;Fail → /no-permission" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
          <mxGeometry x="510" y="730" width="430" height="90" as="geometry"/>
        </mxCell>

        <mxCell id="gatePortal" value="User Portal UI&#10;No role gate&#10;(any authenticated user)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
          <mxGeometry x="980" y="730" width="380" height="90" as="geometry"/>
        </mxCell>

        <!-- Authorization layer -->
        <mxCell id="authz" value="Authorization / Permissions (runtime checks)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontStyle=1;" vertex="1" parent="1">
          <mxGeometry x="340" y="850" width="740" height="50" as="geometry"/>
        </mxCell>

        <mxCell id="authzAdmin" value="Admin Center&#10;- permissions claim → canAccessRoute()&#10;- backend: planned hard auth (currently permissive)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="1">
          <mxGeometry x="80" y="930" width="380" height="90" as="geometry"/>
        </mxCell>

        <mxCell id="authzDev" value="Developer WS&#10;- backend method guard: @RequireDeveloperPermission&#10;- permission source: Admin Center developer-permissions API / token" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="1">
          <mxGeometry x="510" y="930" width="430" height="100" as="geometry"/>
        </mxCell>

        <mxCell id="authzPortal" value="User Portal&#10;- business/visibility checks via Admin Center APIs&#10;  (/users/{id}/roles|virtual-groups|business-units ...)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="1">
          <mxGeometry x="980" y="930" width="380" height="90" as="geometry"/>
        </mxCell>

        <!-- Edges -->
        <mxCell id="e1" style="endArrow=block;html=1;strokeColor=#6c8ebf;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="auth" target="jwt">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e2" style="endArrow=block;html=1;strokeColor=#82b366;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="identity" target="directRoles">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e3" style="endArrow=block;html=1;strokeColor=#82b366;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="roleCatalog" target="directRoles">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e4" style="endArrow=block;html=1;strokeColor=#82b366;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="identity" target="vgRoles">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e5" style="endArrow=block;html=1;strokeColor=#82b366;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="roleCatalog" target="vgRoles">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e6" style="endArrow=block;html=1;strokeColor=#82b366;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="identity" target="buRoles">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e7" style="endArrow=block;html=1;strokeColor=#82b366;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="roleCatalog" target="buRoles">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e8" style="endArrow=block;html=1;strokeColor=#b85450;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="directRoles" target="effective">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e9" style="endArrow=block;html=1;strokeColor=#b85450;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="vgRoles" target="effective">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e10" style="endArrow=block;html=1;strokeColor=#b85450;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="buRoles" target="effective">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e11" style="endArrow=block;html=1;strokeColor=#d6b656;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="effective" target="jwt">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e12" style="endArrow=block;html=1;strokeColor=#6c8ebf;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="jwt" target="gateAdmin">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e13" style="endArrow=block;html=1;strokeColor=#6c8ebf;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="jwt" target="gateDev">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e14" style="endArrow=block;html=1;strokeColor=#6c8ebf;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="jwt" target="gatePortal">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e15" style="endArrow=block;html=1;strokeColor=#d6b656;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="gateAdmin" target="authzAdmin">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e16" style="endArrow=block;html=1;strokeColor=#d6b656;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="gateDev" target="authzDev">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

        <mxCell id="e17" style="endArrow=block;html=1;strokeColor=#d6b656;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="gatePortal" target="authzPortal">
          <mxGeometry relative="1" as="geometry"/>
        </mxCell>

      </root>
    </mxGraphModel>
  </diagram>
</mxfile>

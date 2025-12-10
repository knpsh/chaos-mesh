# Chaos Mesh -- Yandex Cloud Downstream Fork

This repository is a downstream fork of the official Chaos Mesh project.

-   **Upstream:** https://github.com/chaos-mesh/chaos-mesh
-   **Downstream owner:** https://github.com/knpsh
-   **Purpose:** Add Yandex Cloud (YC) chaos engineering support

This fork follows a **long-term rebase-based downstream maintenance
model** suitable for enterprise use, auditing, and long-term lifecycle
management.

------------------------------------------------------------------------

## 1. Branch Model

| Branch          | Description                                                      |
|-----------------|------------------------------------------------------------------|
| `master`        | Clean mirror of upstream `chaos-mesh/chaos-mesh:master`          |
| `yandex-cloud`  | Downstream branch containing Yandex Cloud support                |

Rules:

-   `master` must always remain a **bit-for-bit** copy of upstream.
-   All YC-specific changes live in `yandex-cloud`.
-   Upstream updates are applied via **rebasing**, not merging.
-   No development work is performed directly on `master`.

------------------------------------------------------------------------

## 2. Downstream Commit Set (YC Patch-Set)

These commits exist **only** in the downstream fork and represent all
Yandex Cloud functionality:

``` text
6fdb9df9 feat: add Yandex Cloud chaos support
bef7c2fd docs: CHANGELOG
80047ace fix: go mod tidy
b5490607 fix: fix test
```

------------------------------------------------------------------------

## 3. File-Level Change Surface

``` text
CHANGELOG.md
api/v1alpha1/ycchaos_types.go
api/v1alpha1/zz_generated.chaosmesh.go
api/v1alpha1/zz_generated.chaosmesh_test.go
api/v1alpha1/zz_generated.deepcopy.go
api/v1alpha1/zz_generated.schedule.chaosmesh.go
api/v1alpha1/zz_generated.workflow.chaosmesh.go
api/v1alpha1/zz_generated.workflow.chaosmesh_test.go
config/crd/bases/chaos-mesh.org_schedules.yaml
config/crd/bases/chaos-mesh.org_workflownodes.yaml
config/crd/bases/chaos-mesh.org_workflows.yaml
config/crd/bases/chaos-mesh.org_ycchaos.yaml
config/crd/kustomization.yaml
controllers/chaosimpl/fx.go
controllers/chaosimpl/ycchaos/common/utils.go
controllers/chaosimpl/ycchaos/common/utils_test.go
controllers/chaosimpl/ycchaos/computerestart/impl.go
controllers/chaosimpl/ycchaos/computestop/impl.go
controllers/chaosimpl/ycchaos/impl.go
controllers/types/types.go
e2e-test/go.mod
e2e-test/go.sum
go.mod
go.sum
helm/chaos-mesh/crds/chaos-mesh.org_schedules.yaml
helm/chaos-mesh/crds/chaos-mesh.org_workflownodes.yaml
helm/chaos-mesh/crds/chaos-mesh.org_workflows.yaml
helm/chaos-mesh/crds/chaos-mesh.org_ycchaos.yaml
manifests/crd.yaml
pkg/dashboard/apiserver/event/event.go
pkg/dashboard/apiserver/experiment/experiment.go
pkg/dashboard/collector/collector.go
pkg/dashboard/collector/schedule_collector.go
pkg/dashboard/swaggerdocs/docs.go
pkg/dashboard/swaggerdocs/swagger.json
pkg/dashboard/swaggerdocs/swagger.yaml
pkg/selector/selector.go
pkg/selector/yc/selector.go
ui/app/src/api/zz_generated.frontend.chaos-mesh.ts
ui/app/src/components/NewExperiment/types.ts
ui/app/src/components/NewExperimentNext/Step2.tsx
ui/app/src/components/NewExperimentNext/data/types.ts
ui/app/src/components/NewWorkflowNext/utils/convert.ts
ui/app/src/components/Scope/index.tsx
ui/app/src/formik/YCChaos.ts
ui/app/src/formik/actions.ts
ui/app/src/i18n/en.json
ui/app/src/i18n/zh.json
ui/app/src/images/chaos/yc.svg
ui/app/src/lib/byKind.tsx
ui/app/src/lib/formikhelpers.ts
ui/app/src/openapi/index.msw.ts
ui/app/src/openapi/index.schemas.ts
ui/app/src/openapi/index.ts
ui/packages/openapi/index.js
```

------------------------------------------------------------------------

## 4. Upstream Sync & Rebase

``` bash
git checkout master
git fetch upstream
git reset --hard upstream/master
git push origin master --force

git checkout yandex-cloud
git rebase master
```

------------------------------------------------------------------------

## 5. Downstream Tag

``` text
yc-initial-integration
```

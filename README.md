# Create Helm Chart:
helm create NAME [flags]
`helm create matomo`
mv matomo chart

# template the chart
`helm template -f chart/values-local.yaml matomo chart/`

# template, and apply the chart
`kubectl create ns matomo-local`
`helm template -n matomo-local -f chart/values-local.yaml matomo chart/ | kubectl apply -f -`





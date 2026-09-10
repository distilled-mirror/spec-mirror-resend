> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Introduction

> A collection of answers to frequently asked questions.

## Domains & Verification

<CardGroup cols={2}>
  <Card title="How do I avoid conflicts with my MX records?" href="/docs/knowledge-base/how-do-i-avoid-conflicting-with-my-mx-records">
    Add DNS records without conflicting with existing MX records.
  </Card>

  <Card title="What if my domain is not verifying?" href="/docs/knowledge-base/what-if-my-domain-is-not-verifying">
    What to do when your domain isn't verifying.
  </Card>
</CardGroup>

## DNS Guides

Step-by-step instructions for verifying your domain with popular DNS providers.

<CardGroup cols={3}>
  <Card
    title="Cloudflare DNS Guide"
    icon={
<svg
  className="h-6 w-6"
  viewBox="0 0 24 24"
  fill="currentColor"
  xmlns="http://www.w3.org/2000/svg"
>
  <path d="M16.5088 16.8447c.1475-.5068.0908-.9707-.1553-1.3154-.2246-.3164-.6045-.499-1.0615-.5205l-8.6592-.1123a.1559.1559 0 0 1-.1333-.0713c-.0283-.042-.0351-.0986-.021-.1553.0278-.084.1123-.1484.2036-.1562l8.7359-.1123c1.0351-.0489 2.1601-.8868 2.5537-1.9136l.499-1.3013c.0215-.0561.0293-.1128.0147-.168-.5625-2.5463-2.835-4.4453-5.5499-4.4453-2.5039 0-4.6284 1.6177-5.3876 3.8614-.4927-.3658-1.1187-.5625-1.794-.499-1.2026.119-2.1665 1.083-2.2861 2.2856-.0283.31-.0069.6128.0635.894C1.5683 13.171 0 14.7754 0 16.752c0 .1748.0142.3515.0352.5273.0141.083.0844.1475.1689.1475h15.9814c.0909 0 .1758-.0645.2032-.1553l.12-.4268zm2.7568-5.5634c-.0771 0-.1611 0-.2383.0112-.0566 0-.1054.0415-.127.0976l-.3378 1.1744c-.1475.5068-.0918.9707.1543 1.3164.2256.3164.6055.498 1.0625.5195l1.8437.1133c.0557 0 .1055.0263.1329.0703.0283.043.0351.1074.0214.1562-.0283.084-.1132.1485-.204.1553l-1.921.1123c-1.041.0488-2.1582.8867-2.5527 1.914l-.1406.3585c-.0283.0713.0215.1416.0986.1416h6.5977c.0771 0 .1474-.0489.169-.126.1122-.4082.1757-.837.1757-1.2803 0-2.6025-2.125-4.727-4.7344-4.727" />
</svg>
}
    href="/knowledge-base/cloudflare"
  />

  <Card
    title="Gandi DNS Guide"
    icon={
<svg
  className="h-6 w-6"
  viewBox="0 0 24 24"
  fill="currentColor"
  xmlns="http://www.w3.org/2000/svg"
>
  <path d="M16.72 5.908a1.496 1.496 0 1 1 2.442 1.729c-.871 1.23-1.906 2.176-3.082 2.82-.661.436-1.414.844-2.209 1.274-.689.373-1.401.758-2.065 1.171-1.565.974-2.46 1.87-2.814 2.82-.473 1.266-.26 2.322.002 2.985a3.8 3.8 0 0 0 1.79 2.006c.808.413 1.931.39 2.93-.06.924-.415 1.542-1.11 1.612-1.813.07-.71-.24-1.114-.553-1.255-.368-.165-.788.006-1.152.467a1.495 1.495 0 1 1-2.349-1.854c1.227-1.554 3.082-2.08 4.726-1.342 1.588.713 2.493 2.392 2.305 4.28-.179 1.792-1.435 3.38-3.36 4.246-1.836.826-3.899.824-5.52-.005a6.8 6.8 0 0 1-3.212-3.572c-.642-1.625-.65-3.446-.022-5.13.605-1.62 1.869-2.803 3.037-3.647a8 8 0 0 1-.828-.33c-1.376-.638-2.573-1.668-3.56-3.061A1.496 1.496 0 0 1 7.28 5.908c.69.976 1.467 1.654 2.376 2.075.69.319 1.457.487 2.344.514.888-.027 1.656-.195 2.345-.514q.098-.045.194-.096.106-.053.208-.112c.738-.424 1.387-1.038 1.972-1.867M11.2 4.17c.191.192.447.297.717.297.271 0 .526-.105.718-.297s.297-.446.297-.717a1 1 0 0 0-.298-.718 1 1 0 0 0-.717-.297c-.27 0-.526.105-.717.297a1 1 0 0 0-.297.718c0 .27.105.525.297.717M9.476 1.011A3.43 3.43 0 0 1 11.917 0c.922 0 1.79.359 2.442 1.01a3.43 3.43 0 0 1 1.01 2.443c0 .922-.358 1.789-1.01 2.44a3.43 3.43 0 0 1-2.442 1.012 3.43 3.43 0 0 1-2.44-1.011 3.43 3.43 0 0 1-1.013-2.441c0-.923.36-1.79 1.012-2.442" />
</svg>
}
    href="/knowledge-base/gandi"
  />

  <Card
    title="GoDaddy DNS Guide"
    icon={
<svg
  className="h-6 w-6"
  viewBox="0 0 24 24"
  fill="currentColor"
  xmlns="http://www.w3.org/2000/svg"
>
  <path d="M20.702 2.29c-2.494-1.554-5.778-1.187-8.706.654C9.076 1.104 5.79.736 3.3 2.29c-3.941 2.463-4.42 8.806-1.07 14.167 2.47 3.954 6.333 6.269 9.77 6.226 3.439.043 7.301-2.273 9.771-6.226 3.347-5.361 2.872-11.704-1.069-14.167zM4.042 15.328a12.838 12.838 0 01-1.546-3.541 10.12 10.12 0 01-.336-3.338c.15-1.98.956-3.524 2.27-4.345 1.315-.822 3.052-.87 4.903-.137.281.113.556.24.825.382A15.11 15.11 0 007.5 7.54c-2.035 3.255-2.655 6.878-1.945 9.765a13.247 13.247 0 01-1.514-1.98zm17.465-3.541a12.866 12.866 0 01-1.547 3.54 13.25 13.25 0 01-1.513 1.984c.635-2.589.203-5.76-1.353-8.734a.39.39 0 00-.563-.153l-4.852 3.032a.397.397 0 00-.126.546l.712 1.139a.395.395 0 00.547.126l3.145-1.965c.101.306.203.606.28.916.296 1.086.41 2.214.335 3.337-.15 1.982-.956 3.525-2.27 4.347a4.437 4.437 0 01-2.25.65h-.101a4.432 4.432 0 01-2.25-.65c-1.314-.822-2.121-2.365-2.27-4.347-.074-1.123.039-2.251.335-3.337a13.212 13.212 0 014.05-6.482 10.148 10.148 0 012.849-1.765c1.845-.733 3.586-.685 4.9.137 1.316.822 2.122 2.365 2.271 4.345a10.146 10.146 0 01-.33 3.334z" />
</svg>
}
    href="/knowledge-base/godaddy"
  />

  <Card
    title="DreamHost DNS Guide"
    icon={
<svg
  className="h-6 w-6"
  viewBox="0 0 512 512"
  fill="currentColor"
  xmlns="http://www.w3.org/2000/svg"
  fillRule="evenodd"
  clipRule="evenodd"
>
  <g fillRule="nonzero">
    <path d="M493.647 381.78c-40.289 22.2-86.333 34.534-135.667 33.712-146.356-3.29-261.467-120.867-259-263.934.822-48.512 15.622-93.734 40.289-131.556C61.157 63.58 7.713 144.98 6.069 239.536 2.778 381.78 118.712 500.18 264.246 503.47c97.022 1.644 181.711-46.867 229.4-121.69" />
    <path d="M279.869 8.49c-39.467 0-76.467 9.867-109.356 27.956-20.555 33.712-32.067 72.356-33.711 111.823-2.467 124.156 98.667 226.934 224.467 229.4 37.822 0 80.578-9.044 113.467-27.133 19.733-33.711 31.245-73.178 31.245-115.111C507.625 110.446 405.669 8.49 279.869 8.49z" />
  </g>
</svg>
}
    href="/knowledge-base/dreamhost"
  />

  <Card
    title="Hetzner DNS Guide"
    icon={
<svg
  className="h-6 w-6"
  viewBox="0 0 24 24"
  fill="currentColor"
  xmlns="http://www.w3.org/2000/svg"
>
  <path d="M0 0v24h24V0H0zm4.602 4.025h2.244c.509 0 .716.215.716.717v5.64h8.883v-5.64c0-.509.215-.717.717-.717h2.229c.5 0 .71.23.724.717v14.516c0 .509-.215.717-.717.717h-2.23c-.51 0-.717-.215-.717-.717v-5.735H7.562v5.735c0 .516-.215.717-.716.717H4.602c-.51 0-.717-.208-.717-.717V4.742c0-.509.207-.717.717-.717z" />
</svg>
}
    href="/knowledge-base/hetzner"
  />

  <Card
    title="Hostinger DNS Guide"
    icon={
<svg
  className="h-6 w-6"
  viewBox="0 0 24 24"
  fill="currentColor"
  xmlns="http://www.w3.org/2000/svg"
>
  <path d="M16.415 0v7.16l5.785 3.384V2.949L16.415 0ZM1.8 0v11.237h18.815L14.89 8.09l-7.457-.003V3.024L1.8 0Zm14.615 20.894v-5.019l-7.514-.005c.007.033-5.82-3.197-5.82-3.197l19.119.091V24l-5.785-3.106ZM1.8 13.551v7.343l5.633 2.949v-6.988L1.8 13.551Z" />
</svg>
}
    href="/knowledge-base/hostinger"
  />

  <Card
    title="IONOS DNS Guide"
    icon={
<svg
  className="h-6 w-6"
  viewBox="0 0 24 24"
  fill="currentColor"
  xmlns="http://www.w3.org/2000/svg"
>
  <path d="M22.182 15.499a1.7634 1.7634 0 0 1-.3536-.0358 1.8319 1.8319 0 0 1-1.2086-.8632l-.0066-.012c-.1308-.2616-.0448-.5693.2-.7162a.5236.5236 0 0 1 .2689-.0743.5327.5327 0 0 1 .4632.272.558.558 0 0 0 .018.0299l.0564.0766.0757.0765a.7385.7385 0 0 0 .3453.167.7596.7596 0 0 0 .5954-.136.7206.7206 0 0 0 .299-.5386.7441.7441 0 0 0-.207-.578s-1.5994-1.6612-1.6712-1.7382a1.9604 1.9604 0 0 1-.1929-.229c-.2256-.3198-.2962-.697-.2614-1.0702a1.7361 1.7361 0 0 1 .2253-.7397s.0732-.124.0948-.1554c.0847-.1236.2515-.2834.3658-.3726a1.8813 1.8813 0 0 1 .3069-.1844 1.7494 1.7494 0 0 1 2.2815.7041.5186.5186 0 0 1 .0553.402.5298.5298 0 0 1-.2528.3263.5082.5082 0 0 1-.2593.0705.5283.5283 0 0 1-.46-.2706.6953.6953 0 0 0-.4656-.329.721.721 0 0 0-.5645.1269.688.688 0 0 0-.267.498.6998.6998 0 0 0 .1905.5398l1.6351 1.6862a1.8284 1.8284 0 0 1 .5071 1.3931c-.0465.5243-.3071.9994-.7152 1.3053a1.8425 1.8425 0 0 1-1.0984.369m-5.175-.0006a1.7608 1.7608 0 0 0 1.7585-1.7589v-3.4787a1.7587 1.7587 0 0 0-3.5173 0v3.4786a1.7608 1.7608 0 0 0 1.7587 1.7589m0-5.9342c.3777 0 .6968.319.6968.6967v3.4786a.6977.6977 0 0 1-.6968.6968.6894.6894 0 0 1-.6968-.6968v-3.4786a.6976.6976 0 0 1 .697-.6967m-7.8986.3224v5.0804a.5309.5309 0 0 0 1.0618 0V12.09Zm2.8802 2.0255V9.0328a.531.531 0 0 1 1.0619 0v5.0828zm1.053 2.9406v.1134a.533.533 0 0 1-1.0067.2408L9.1153 9.154v-.1212a.5261.5261 0 0 1 .3028-.4772.5253.5253 0 0 1 .7088.2475Zm-7.9067.6457a1.761 1.761 0 0 0 1.7586-1.7589v-3.4786a1.7587 1.7587 0 0 0-3.5173 0v3.4786a1.7609 1.7609 0 0 0 1.7587 1.7589m0-5.9342a.707.707 0 0 1 .6968.6967v3.4786a.6968.6968 0 1 1-1.3936 0v-3.4786a.6976.6976 0 0 1 .6968-.6967M0 14.9111a.5791.5791 0 1 0 1.1581 0V9.0803a.5791.5791 0 0 0-1.1582 0z" />
</svg>
}
    href="/knowledge-base/ionos"
  />

  <Card
    title="Namecheap DNS Guide"
    icon={
<svg
  className="h-6 w-6"
  viewBox="0 0 24 24"
  fill="currentColor"
  xmlns="http://www.w3.org/2000/svg"
>
  <path d="M17.295 17.484c.227.403.57.728.985.931-.309.15-.647.229-.99.232h-3.068a2.26 2.26 0 0 1-1.957-1.143L6.705 6.511a2.27 2.27 0 0 0-.974-.922c.309-.153.652-.233.997-.232h3.05c.81.003 1.558.438 1.959 1.143l5.558 10.984zm-9.329-7.392L6.269 6.755c-.209-.392-.582-.657-.984-.829-.204.165-.391.35-.522.581-.184.349-4.391 8.648-4.569 8.987a2.245 2.245 0 0 0 4.016 1.999l3.756-7.401zm15.846-1.593a2.245 2.245 0 0 0-1.162-2.955v-.001a2.243 2.243 0 0 0-.892-.187l-.003-.011c-.816 0-1.569.443-1.965 1.157l-3.749 7.414 1.689 3.323c.213.399.59.664.998.839.252-.2.473-.444.605-.742l4.479-8.837z" />
</svg>
}
    href="/knowledge-base/namecheap"
  />

  <Card
    title="Porkbun DNS Guide"
    icon={
<svg
  className="h-6 w-6"
  viewBox="0 0 24 24"
  fill="currentColor"
  xmlns="http://www.w3.org/2000/svg"
>
  <path d="M12 0C5.3708 0 .0176 5.3532.0176 11.9824.0176 18.6117 5.3708 24 12 24s11.9824-5.3532 11.9824-11.9824C23.9824 5.3883 18.6292 0 12 0ZM5.832 5.8848c1.0635.2481 2.092.6384 3.0137 1.1347-1.099.5318-1.9866 1.3824-2.6602 2.375-.4254-.5672-.6738-1.2767-.6738-2.0566 0-.5318.1076-.9923.3203-1.4531zm12.336 0c.2127.4254.3203.9213.3203 1.453 0 .78-.2484 1.4895-.6738 2.0567-.6736-.9926-1.5967-1.8432-2.6602-2.375a9.9821 9.9821 0 0 1 3.0137-1.1347zm-6.0723.8105c3.5286.0471 6.3547 2.9198 6.3203 6.457v3.8282c0 .638-.5318 1.1699-1.17 1.1699-.638 0-1.1698-.5318-1.1698-1.17v-.957H7.8516v.957c0 .6382-.5319 1.17-1.17 1.17-.638 0-1.1699-.5318-1.1699-1.17v-3.6503c0-3.5096 2.7307-6.489 6.2403-6.6309.1152-.0044.2299-.0054.3437-.0039zm1.5 3.7988c-.4963 0-.9219.4256-.9219.922 0 .248.0711.4242.213.6015.1417.2127.3536.3546.5663.461-.1418.0708-.3188.1425-.496.1425-.2128 0-.3907.176-.3907.3887s.178.3906.3906.3906h.1778c.6026 0 1.1346-.3553 1.3828-.8516.39-.1418.7092-.3896.9219-.7441.0709-.1064.0337-.2484-.0372-.2129-.1063-.0355-.2123-.034-.2832.0723-.1063.1418-.2485.2826-.4257.3535v-.1426c0-.39-.1409-.7086-.3536-.9922-.1772-.2481-.425-.3887-.7441-.3887zm0 .5313c.2127 0 .3532.1408.3887.3535v.1777c0 .1773-.0346.3543-.1055.4961-.2481-.0709-.4617-.213-.6035-.4257-.0355-.071-.0703-.14-.0703-.211 0-.2392.2063-.3906.3906-.3906z" />
</svg>
}
    href="/knowledge-base/porkbun"
  />

  <Card
    title="Route 53 DNS Guide"
    icon={
<svg
  className="h-6 w-6"
  viewBox="0 0 24 24"
  fill="currentColor"
  xmlns="http://www.w3.org/2000/svg"
>
  <path d="M6.763 10.036c0 .296.032.535.088.71.064.176.144.368.256.576.04.063.056.127.056.183 0 .08-.048.16-.152.24l-.503.335a.383.383 0 0 1-.208.072c-.08 0-.16-.04-.239-.112a2.47 2.47 0 0 1-.287-.375 6.18 6.18 0 0 1-.248-.471c-.622.734-1.405 1.101-2.347 1.101-.67 0-1.205-.191-1.596-.574-.391-.384-.59-.894-.59-1.533 0-.678.239-1.23.726-1.644.487-.415 1.133-.623 1.955-.623.272 0 .551.024.846.064.296.04.6.104.918.176v-.583c0-.607-.127-1.03-.375-1.277-.255-.248-.686-.367-1.3-.367-.28 0-.568.031-.863.103-.295.072-.583.16-.862.272a2.287 2.287 0 0 1-.28.104.488.488 0 0 1-.127.023c-.112 0-.168-.08-.168-.247v-.391c0-.128.016-.224.056-.28a.597.597 0 0 1 .224-.167c.279-.144.614-.264 1.005-.36a4.84 4.84 0 0 1 1.246-.151c.95 0 1.644.216 2.091.647.439.43.662 1.085.662 1.963v2.586zm-3.24 1.214c.263 0 .534-.048.822-.144.287-.096.543-.271.758-.51.128-.152.224-.32.272-.512.047-.191.08-.423.08-.694v-.335a6.66 6.66 0 0 0-.735-.136 6.02 6.02 0 0 0-.75-.048c-.535 0-.926.104-1.19.32-.263.215-.39.518-.39.917 0 .375.095.655.295.846.191.2.47.296.838.296zm6.41.862c-.144 0-.24-.024-.304-.08-.064-.048-.12-.16-.168-.311L7.586 5.55a1.398 1.398 0 0 1-.072-.32c0-.128.064-.2.191-.2h.783c.151 0 .255.025.31.08.065.048.113.16.16.312l1.342 5.284 1.245-5.284c.04-.16.088-.264.151-.312a.549.549 0 0 1 .32-.08h.638c.152 0 .256.025.32.08.063.048.12.16.151.312l1.261 5.348 1.381-5.348c.048-.16.104-.264.16-.312a.52.52 0 0 1 .311-.08h.743c.127 0 .2.065.2.2 0 .04-.009.08-.017.128a1.137 1.137 0 0 1-.056.2l-1.923 6.17c-.048.16-.104.263-.168.311a.51.51 0 0 1-.303.08h-.687c-.151 0-.255-.024-.32-.08-.063-.056-.119-.16-.15-.32l-1.238-5.148-1.23 5.14c-.04.16-.087.264-.15.32-.065.056-.177.08-.32.08zm10.256.215c-.415 0-.83-.048-1.229-.143-.399-.096-.71-.2-.918-.32-.128-.071-.215-.151-.247-.223a.563.563 0 0 1-.048-.224v-.407c0-.167.064-.247.183-.247.048 0 .096.008.144.024.048.016.12.048.2.08.271.12.566.215.878.279.319.064.63.096.95.096.502 0 .894-.088 1.165-.264a.86.86 0 0 0 .415-.758.777.777 0 0 0-.215-.559c-.144-.151-.416-.287-.807-.415l-1.157-.36c-.583-.183-1.014-.454-1.277-.813a1.902 1.902 0 0 1-.4-1.158c0-.335.073-.63.216-.886.144-.255.335-.479.575-.654.24-.184.51-.32.83-.415.32-.096.655-.136 1.006-.136.175 0 .359.008.535.032.183.024.35.056.518.088.16.04.312.08.455.127.144.048.256.096.336.144a.69.69 0 0 1 .24.2.43.43 0 0 1 .071.263v.375c0 .168-.064.256-.184.256a.83.83 0 0 1-.303-.096 3.652 3.652 0 0 0-1.532-.311c-.455 0-.815.071-1.062.223-.248.152-.375.383-.375.71 0 .224.08.416.24.567.159.152.454.304.877.44l1.134.358c.574.184.99.44 1.237.767.247.327.367.702.367 1.117 0 .343-.072.655-.207.926-.144.272-.336.511-.583.703-.248.2-.543.343-.886.447-.36.111-.734.167-1.142.167zM21.698 16.207c-2.626 1.94-6.442 2.969-9.722 2.969-4.598 0-8.74-1.7-11.87-4.526-.247-.223-.024-.527.272-.351 3.384 1.963 7.559 3.153 11.877 3.153 2.914 0 6.114-.607 9.06-1.852.439-.2.814.287.383.607zM22.792 14.961c-.336-.43-2.22-.207-3.074-.103-.255.032-.295-.192-.063-.36 1.5-1.053 3.967-.75 4.254-.399.287.36-.08 2.826-1.485 4.007-.215.184-.423.088-.327-.151.32-.79 1.03-2.57.695-2.994z" />
</svg>
}
    href="/knowledge-base/route53"
  />

  <Card
    title="Squarespace DNS Guide"
    icon={
<svg
  className="h-6 w-6"
  viewBox="0 0 24 24"
  fill="currentColor"
  xmlns="http://www.w3.org/2000/svg"
>
  <path d="M22.655 8.719c-1.802-1.801-4.726-1.801-6.564 0l-7.351 7.35c-.45.45-.45 1.2 0 1.65.45.449 1.2.449 1.65 0l7.351-7.351c.899-.899 2.362-.899 3.264 0 .9.9.9 2.364 0 3.264l-7.239 7.239c.9.899 2.362.899 3.263 0l5.589-5.589c1.836-1.838 1.836-4.763.037-6.563zm-2.475 2.437c-.451-.45-1.201-.45-1.65 0l-7.354 7.389c-.9.899-2.361.899-3.262 0-.45-.45-1.2-.45-1.65 0s-.45 1.2 0 1.649c1.801 1.801 4.726 1.801 6.564 0l7.351-7.35c.449-.487.449-1.239.001-1.688zm-2.439-7.35c-1.801-1.801-4.726-1.801-6.564 0l-7.351 7.351c-.45.449-.45 1.199 0 1.649s1.2.45 1.65 0l7.395-7.351c.9-.899 2.371-.899 3.27 0 .451.45 1.201.45 1.65 0 .421-.487.421-1.199-.029-1.649h-.021zm-2.475 2.437c-.45-.45-1.2-.45-1.65 0l-7.351 7.389c-.899.9-2.363.9-3.265 0-.9-.899-.9-2.363 0-3.264l7.239-7.239c-.9-.9-2.362-.9-3.263 0L1.35 8.719c-1.8 1.8-1.8 4.725 0 6.563 1.801 1.801 4.725 1.801 6.564 0l7.35-7.351c.451-.488.451-1.238 0-1.688h.002z" />
</svg>
}
    href="/knowledge-base/squarespace"
  />

  <Card
    title="Strato DNS Guide"
    icon={
<svg
  className="h-6 w-6"
  viewBox="0 0 139 139"
  fill="none"
  xmlns="http://www.w3.org/2000/svg"
>
  <path
    d="M138.92 19.8467C138.92 8.88382 130.036 0 119.075 0H49.6143C49.6144 10.9579 58.4987 19.8466 69.46 19.8467H109.151C114.631 19.8467 119.075 24.2901 119.075 29.7695L119.073 69.4629C119.073 80.4222 127.958 89.3086 138.919 89.3086L138.92 19.8467ZM89.3057 138.926C94.785 138.926 99.2284 134.483 99.2285 129.002V49.6172C99.2285 44.1368 94.7851 39.6924 89.3057 39.6924H9.92188C4.44155 39.6925 0 44.1368 0 49.6172V129.002C0.000110772 134.483 4.44161 138.926 9.92188 138.926H89.3057Z"
    fill="currentColor"
  />
</svg>
}
    href="/knowledge-base/strato"
  />

  <Card
    title="Vercel DNS Guide"
    icon={
<svg
  className="h-6 w-6"
  viewBox="0 0 24 24"
  fill="currentColor"
  xmlns="http://www.w3.org/2000/svg"
>
  <path d="m12 1.608 12 20.784H0Z" />
</svg>
}
    href="/knowledge-base/vercel"
  />
</CardGroup>

## Deliverability

<CardGroup cols={2}>
  <Card title="How do I avoid Gmail's spam folder?" href="/docs/knowledge-base/how-do-i-avoid-gmails-spam-folder">
    Learn how to improve inbox placement in Gmail.
  </Card>

  <Card title="Why Are My Emails Going to Spam?" href="/docs/knowledge-base/why-are-my-emails-going-to-spam">
    Troubleshoot emails landing in spam or getting quarantined.
  </Card>

  <Card title="Is it better to send from a subdomain or root domain?" href="/docs/knowledge-base/is-it-better-to-send-emails-from-a-subdomain-or-the-root-domain">
    Discover why sending emails from a subdomain can be better than using a root
    domain.
  </Card>

  <Card title="Why are my emails landing on the suppression list?" href="/docs/knowledge-base/why-are-my-emails-landing-on-the-suppression-list">
    Learn why your emails land on the suppression list, and how to remove them.
  </Card>

  <Card title="Domain and IP Warm-up Guide" href="/docs/knowledge-base/warming-up">
    Learn how to warm up your domain and dedicated IP for optimal deliverability.
  </Card>
</CardGroup>

## Sending

<CardGroup cols={2}>
  <Card title="Account Quotas and Limits" href="/docs/knowledge-base/account-quotas-and-limits">
    Understand the sending quotas and rate limits for your Resend account.
  </Card>

  <Card title="How do Dedicated IPs Work?" href="/docs/knowledge-base/how-do-dedicated-ips-work">
    Learn how Dedicated IPs work and how to request them.
  </Card>

  <Card title="What sending feature should I use?" href="/docs/knowledge-base/what-sending-feature-to-use">
    Find the right Resend feature for your email sending use case.
  </Card>

  <Card title="Should I add an unsubscribe link?" href="/docs/knowledge-base/should-i-add-an-unsubscribe-link">
    Learn when to add unsubscribe links to your transactional and marketing
    emails.
  </Card>
</CardGroup>

## Tutorials

<CardGroup cols={2}>
  <Card title="Maximize deliverability for Supabase Auth emails" href="/docs/knowledge-base/how-do-i-maximize-deliverability-for-supabase-auth-emails">
    Everything you should do before sending authentication emails with Resend and
    Supabase.
  </Card>

  <Card title="How do I set up Apple Branded Mail?" href="/docs/knowledge-base/how-do-i-set-up-apple-branded-mail">
    Display your brand logo in the Apple Mail inbox.
  </Card>

  <Card title="How do I send with an avatar?" href="/docs/knowledge-base/how-do-i-send-with-an-avatar">
    Learn how to show your avatar in the inbox of your recipients.
  </Card>

  <Card title="Forward emails with Resend Inbound" href="/docs/knowledge-base/forward-emails-with-resend-inbound">
    Set up email forwarding using Resend's inbound email processing.
  </Card>

  <Card title="Template emails with React Email" href="/docs/knowledge-base/template-emails-with-react-email">
    Author email templates as React components and upload them to Resend with the
    CLI.
  </Card>

  <Card title="Embed the React Email editor" href="/docs/knowledge-base/embed-react-email-editor">
    Add the open-source visual email editor to your own application.
  </Card>
</CardGroup>

## Troubleshooting

<CardGroup cols={3}>
  <Card title="How do I fix CORS issues?" href="/docs/knowledge-base/how-do-i-fix-cors-issues">
    Recommended options to avoid CORS errors when sending emails.
  </Card>

  <Card title="403 Error: Domain Mismatch" href="/docs/knowledge-base/403-error-domain-mismatch">
    Resolve 403 errors when the sending domain doesn't match your verified domain.
  </Card>

  <Card title="Domain Already Registered by Another Account" href="/docs/knowledge-base/domain-already-registered">
    Resolve domain ownership conflicts when a domain is already registered.
  </Card>

  <Card title="Email says delivered but not received?" href="/docs/knowledge-base/what-if-an-email-says-delivered-but-the-recipient-has-not-received-it">
    Steps to take when an email is delivered but the recipient hasn't received it.
  </Card>
</CardGroup>

## AI Tools

<CardGroup cols={2}>
  <Card title="AI Onboarding" href="/docs/ai-onboarding">
    Everything you need to onboard your AI agent to Resend.
  </Card>

  <Card title="MCP Server" href="/docs/mcp-server">
    Use Resend's Model Context Protocol server to send emails from AI tools.
  </Card>

  <Card title="Email Best Practices Skills" href="/docs/email-best-practices-skill">
    Skills for AI agents to build production-ready email systems with Resend.
  </Card>

  <Card title="React Email Skill" href="/docs/react-email-skill">
    Skills for AI agents to build HTML emails using React components with Resend.
  </Card>

  <Card title="Resend Skill" href="/docs/resend-skill">
    Skills for AI agents to send emails with Resend.
  </Card>
</CardGroup>

## Account Management

<CardGroup cols={3}>
  <Card title="What is Resend Pricing?" href="/docs/knowledge-base/what-is-resend-pricing">
    Learn more about Resend's pricing plans.
  </Card>

  <Card title="How can I delete my Resend account?" href="/docs/knowledge-base/how-can-i-delete-my-resend-account">
    Learn how to permanently delete your Resend account and data.
  </Card>

  <Card title="How to handle API keys" href="/docs/knowledge-base/how-to-handle-api-keys">
    Best practices for managing and securing your Resend API keys.
  </Card>

  <Card title="How to handle a leaked API key" href="/docs/knowledge-base/how-to-handle-a-leaked-api-key">
    What to do when an API key is exposed or used without authorization.
  </Card>

  <Card title="How to add multi-factor authentication to your Resend account" href="/docs/knowledge-base/how-can-i-add-mfa">
    Enable or disable multi-factor authentication (MFA) or two-factor
    authentication (2FA) on your Resend account.
  </Card>
</CardGroup>

## Testing

<CardGroup cols={2}>
  <Card title="E2E Testing with Playwright" href="/docs/knowledge-base/end-to-end-testing-with-playwright">
    Set up end-to-end email testing with Playwright and Resend.
  </Card>

  <Card title="What email addresses to use for testing?" href="/docs/knowledge-base/what-email-addresses-to-use-for-testing">
    Use Resend's test email addresses to simulate different delivery scenarios.
  </Card>
</CardGroup>

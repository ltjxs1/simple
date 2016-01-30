# simple

  #新浪邮件服务器
  spring.mail.host=smtp.sina.com
  spring.mail.port=25
  spring.mail.username=jzpwork@sina.cn
  #Email密码
  spring.mail.password=****
  
  
  @NonRest
  @RequestMapping(value = "/p", method = RequestMethod.GET)
  public Object p() {
      service.sendMail();
      return null;
    }
  
    @Autowired
    private JavaMailSenderImpl mailSender;

    public void sendMail() {
        MimeMessage mimeMessage = mailSender.createMimeMessage();
        try {
            MimeMessageHelper helper = new MimeMessageHelper(mimeMessage, true);
            helper.setFrom("jzpwork@sina.cn");
            helper.setTo("jiangzhipeng@boxfish.cn");
            helper.setText("hello world!");
            ClassPathResource file = new ClassPathResource("/static/单词批量导入模板.xlsx");
            helper.addAttachment("单词批量导入模板.xlsx", file);
            mailSender.send(mimeMessage);
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }  
    
    
